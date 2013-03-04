==Overview==

A key value store. If a requested value is unknown or needs to be refreshed it calls out to an executable based upon convention. 

For example running

alexandria -f -q jim.bob

Will look for and run

 /var/lib/alexandria/exec/jim/bob

If that doesn't exist it will run

/var/lib/alexandria/input/exec/jim -q bob

And cache whatever is returned in a mdb if it is successful.

Without the -f it will only refresh the value if it didn't exist in the database or the parameters for its refresh had been exceeded.

There will also be a daemonised version which takes queries over tcp and listens for invalidations of data or potentially new data.

You can also ask for a consistent data set in some fashion so all queries with a given data set stamp get the same values for the queries.   

It can also run scripts (or notify?) if a value changes. If the flag was set it would pipe the value acquired to  

/var/lib/alexandria/output/exec/jim/bob or jim -q bob if it didn't exist.


It is envisaged that /var/lib/alexandria/input/net would generally have a program on that passed on requests to other hosts running alexandria. Through whatever method/security level you choose. So a virtualisation platform could ask an iscsi host what volumes it had available. 



==Vision==

Configuration management tools tend to be too monolithic

The basic idea is that there is an analogy between the model view controller model and configuration management.

The model is all the data about your computers and the network.

The controller takes information from the models and passes it onto the view

The views are configuration files and system state.

We may want the same reactivity as originally envisaged, when something in the mmodel changes the view also changes.


Anyway this project is the first steps in creating a quick unified model.

==Goals==

1) Separation of concerns

This will do one thing well. It stores information so that if two bits of configuration management need the same bit of data they don't have to generate it twice.

2) Re-use. 

The information gathering modules for the system can be reused by different people. As it stands different peoples puppet configuation files are generally incompatible as. These are always likely to be different. However they are likely to use information from similar sources. And end up creating similar files (but that is another project).


It could even be used to gather information to do static web page generation.

3) IO is the killer for a speedy run. 

Information needed for configuration managemnent may be spread across the network, or acquired by slow scripts. We want to cache these values perhaps only having them updated when needed or when load is low.

However these questions are not something the model should have to deal with, it should gain instruction from the controller about what to do.








