## General
+ Use ENUMS instead of magic numbers

##### Naming Conventions
We generally follow a Pascal naming convention
+ ThisIsPascal Naming Convention.
+ thisIsCamelCase.
+ Function variables are camel cased.
+ Boolean variables should use the word, is or has.
+ Private variables/function names should start with "_"

##### Functions
+ Functions should preferably be Pure, meaning that they should not modify their inputs.
+ Summary of function, comments

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
[Link1](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions)
[Link2](https://referencesource.microsoft.com/#mscorlib/system/collections/stack.cs)


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

#### MYSQL

##### Naming Convention 
[Link1](https://dev.mysql.com/doc/dev/mysql-server/latest/PAGE_NAMING_CONVENTIONS.html)
[Link2](https://www.sqlstyle.guide/)
+ Keywords/Reserved words should be used in CAPITALS, e.g. SELECT, INNER JOIN, WHERE
+ This should be followed in table schema as well as queries SPs/Functions.
+ Ensure the name is unique and does not exist as a reserved keyword.
+ Names must begin with a letter and may not end with an underscore
+ Only use letters, numbers and underscores in names.

##### Tables
+ Use a collective name or, less ideally, a plural form. For example (in order of preference) staff and employees.
+ Never give a table the same name as one of its columns and vice versa.
+ Avoid, where possible, concatenating two table names together to create the name of a relationship table. Rather than cars_mechanics prefer services.
+ Table names should not have dot (.) and all should be all small letters. Although we have a lot of table names in our DB with dot in them but this should be avoided going forward.

##### Columns
+ Always use the singular name.
+ Do not add a column with the same name as its table and vice versa.
+ Column names should be in PascalCase e.g. QuestionId, SurveyId.

##### Store Procedures
Follow the following format while writing queries in SPs:

    # Resultset - 1 - Project Details   
    SELECT
            p.ProjectId,
            p.Project as ProjectName,
            IFNULL(p.ProjectTypeId,0) as ProjectTypeId,
            typ.ProjectType,
            IFNULL(p.ProjectTechnologyId,0) as TechnologyId,
            tch.ProjectTechnology as Technology,                        
            p.Description,
        IFNULL(p.ProjectStatusId,0) as ProjectStatusId,
        st.ProjectStatus,
        IFNULL(p.ProjectOwnerId,0) as ProjectOwnerId,
        own.Name as ProjectOwner,
        IFNULL(tmp.TemplateId,0) as TemplateId,
        tmp.TemplateName as Template,
        p.StartDate
FROM
        projects p
LEFT JOIN
        project_status st ON p.ProjectStatusId = st.ProjectStatusId
LEFT JOIN
        project_types typ ON p.ProjectTypeId = typ.ProjectTypeId
LEFT JOIN
        project_technologies tch ON p.ProjectTechnologyId = tch.ProjectTechnologyId
LEFT JOIN
        org_entities own ON p.ProjectOwnerId = own.OrgEntityId        
LEFT JOIN
        templates tmp ON p.TemplateId = tmp.TemplateId
WHERE
        p.ProjectId = pId
;

##### Query syntax
+ Always use uppercase for the reserved keywords like SELECT and WHERE.

##### MYSQL GROUP BY OR DISTINCT which one is Better ?
[Link](https://stackoverflow.com/questions/581521/whats-faster-select-distinct-or-group-by-in-mysql)
They are essentially equivalent to each other (in fact this is how some databases implement DISTINCT under the hood).

If one of them is faster, it's going to be DISTINCT. This is because, although the two are the same, a query optimizer would have to catch the fact that your GROUP BY is not taking advantage of any group members, just their keys. DISTINCT makes this explicit, so you can get away with a slightly dumber optimizer.

