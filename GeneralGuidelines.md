## General

##### Naming Conventions
We generally follow a Pascal naming convention
+ ThisIsPascal Naming Convention.
+ thisIsCamelCase.
+ Function variables are camel cased.
+ Boolean variables should use the word, is or has.

##### Functions
Functions should preferably be Pure, meaning that they should not modify their inputs.

##### DRY Principles

##### SOLID Principles
Learn them, and use them often.

###### Single Responsibility
A function should be doing one thing idealy. I mean, if a function is fetching data, then transforming it, that's two things. Helps with readability, and testing.

    this.sharedService.fetchData(params)
        .subscribe((data: any) => {
        
            this.data = data;
            // this below or any subsequent code should have been part of a separate function
            this.data.forEach((dt: any) => {
                dt.createdBy = '';
            });
        
        });
        
##### Test inputs
Test inputs to functions, a function should not make assumptions about inputs.

##### Early Exit
A function should test early exit conditions before doing writing the longest path.

    if(data.statusCode != Success){
        return;
    }

##### PrimaryID is not supposed to have ID capitalized, it should be Id :)


#### C#

#### Typescript 
+ Functions are public by default, you do not need to specify if public
+ Interface/Class Properties will use Pascal naming convention.
+ Function names will be camel cased
+ Function should always specify return types, if it is not returning anything, then the return type should be void
+ Do not use ANY, unless there is a reason to do so. Ajax return types should not be any.

##### General Guidelines
###### Use find, filter instead of looping to find matching elemnets
    let el = null;
    while(i < array.length) {
        if(array[i].name == 'match') {
            el = array[i];
        }
        i++;
    }
    
can be simplified to:
    let el = array.find(f => f.name == 'match');
Even if you have to use, for or while, it's still prefrable to use forEach (index of iteration is the second paramter).
