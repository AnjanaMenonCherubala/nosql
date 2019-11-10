# NoSQL vClock Project

This solution was implemented by utlizing the multi-threaded programmimg paradigm. There are five queues which have been created with the intent of updating each of the 5 database nodes.

In the event that the cluster has no documents created, new documents will be created in the 'create' case of the sync_document method in the API.java class. 

The vector clocks of the nodes are synced every 5 seconds by design. If the node in question is encountered is sent with a sync request from another node, the following are the parameters which are considered:
1. If the incoming vector clock is a descendant od the present vector clock.
2. If the present vector clock is the descendant of the incoming node request.
3. When neither of the above are true , which is the case of Conflict.

In all the three cases the vector clocks are merged, but in case of the conflict, the node indices of the nodes are compared against each other and the document belonging to the higher node will always emerge as the winnder and the document belongign to this node will be copied into the losing node's document.

                                                                          
