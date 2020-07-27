## Before you start:
1. install the Amplify CLI `npm install -g @aws-amplify/cli`

2. You need to set up your AWS security credentials before the sample code is able
to connect to AWS. You can do this by creating a file named "credentials" at `~/.aws/` 
`(C:\Users\USER_NAME\.aws\ for Windows users)` and saving the following lines in the file:

    ```
    [default]
    aws_access_key_id = <your access key id>
    aws_secret_access_key = <your secret key>
    ```
## connect to the amplify CLI:
1. run this command `amplify init`
2. will ask you if you want to use existing environment, say yes
3. Choose the dev env
4. choose your default code editor
5. will ask you "Do you want to use an AWS profile?" say yes
6. choose a profile you want to use
7. Type amplify Pull
8. Your schema will be at a file with name __schema.graphql__ you can find it at *`\backend\api\connectproject\schema.graphql`* 
9. You can change it if you want and then type `amplify push` in the terminal to push the changes
10. to generate the code (__mutations, queries, subscriptions__) type `amplify codegen add` in the terminal
11. choose the language you want it in



## How to use the api int the frontend
First of all the id, createdAt, and updatedAt are auto-generated to you and you can find those in any record.
Second all records has a field called __owner__ this field used for authorization so the owner of the record can read and write on the record.
How to do some operations on the data:
1. __Student__:
    While you are signed in as a student you can do
    1. create a student record: you will use these steps
        1. Create student record: use these fields 
            - tutorID: __ID*__ of the tutor that this student is assigned to him
            - adminID: __ID*__ of the admin that this student is assigned to him
            - creditsRemaining: __Int*__
            - tutorUserName: __String*__ the username of the tutor that can read the information of this student (the tutor that this student is assigned to him)
        2. Create a profile record: use these fields
            - skypeID: __String__
            - originCity: __String__
            - originCountry: __String__
            - Interest: __String__
            - facts: __String__
            - tutorUserName: __String*__ the username of the tutor that can read the information of this student (the tutor that this student is assigned to him)
        3. Create a user record: use these fields
            - userName: __String*__
            - firstName: __String*__
            - lastName: __String*__
            - email: __String*__
            - avatarUrl: __String*__
            - approved: __Boolean*__
            - profileID: __ID*__
            - userableID: __ID*__
            - tutorUserName: __String__ the username of the tutor that can read the information of this student (the tutor that this student is assigned to him)
            - userableType: __Enum*__
    2. Who has access to it and which:
        - the admin has full access 
        - the user itself has full access
2. __Tutor__:
    While you are signed in as a tutor you can do
    1. create a tutor record: you will use these steps
        1. create a tutor record: you will use these fields
            - adminID: __ID__ of the admin that this student is assigned to him
            - paymentMethodID: __ID__
            - studentsUserNames: [__String__] the usernames of the students who has access to read this record (the students who assigned to this tutor)
        2. Create a profile record: use these fields
            - skypeID: __String__
            - originCity: __String__
            - originCountry: __String__
            - Interest: __String__
            - facts: __String__
            - studentsUserNames: __[String]__ the username of the students that assigned to the tutor so they can access to read the information of this tutor
        3. Create a user record: use these fields
            - userName: __String*__
            - firstName: __String*__
            - lastName: __String*__
            - email: __String*__
            - avatarUrl: __String*__
            - approved: __Boolean*__
            - profileID: __ID*__
            - userableID: __ID*__
            - userableType: __Enum*__
            - studentsUserNames: __[String]__ the username of the students that assigned to the tutor so they can access to read the information of this tutor
    2. Who has access to it and which:
        - the admin has full access 
        - the tutor itself has full access
        - It's students has read access
3. __admin__
     While you are signed in as an admin you can do
    1. create a student record: you will use these steps
        1. create a admin record: you will use these fields
            - supper: __Boolean*__
            - studentsUserNames: [__String__] the usernames of the students who has access to read this record (the students who assigned to this tutor)
            - tutorsUserNames: [__String__] the usernames of the tutors who has access to read this record (the tutors who assigned to this admin)
        2. Create a profile record: use these fields
            - skypeID: __String__
            - originCity: __String__
            - originCountry: __String__
            - Interest: __String__
            - facts: __String__
            - studentsUserNames: [__String__] the usernames of the students who has access to read this record (the students who assigned to this tutor)
            - tutorsUserNames: [__String__] the usernames of the tutors who has access to read this record (the tutors who assigned to this admin)
        3. Create a user record: use these fields
            - userName: __String*__
            - firstName: __String*__
            - lastName: __String*__
            - email: __String*__
            - avatarUrl: __String*__
            - approved: __Boolean*__
            - profileID: __ID*__
            - userableID: __ID*__
            - userableType: __Enum*__ *(Admin, Student, Tutor)*
            - studentsUserNames: [__String__] the usernames of the students who has access to read this record (the students who assigned to this tutor)
            - tutorsUserNames: [__String__] the usernames of the tutors who has access to read this record (the tutors who assigned to this admin)
    2. Who has access to it and which:
        - the admin has full access 
        - It's students has read access
        - It's tutors has read access

3. __session__
    1. to build a new session you will need to input the following fields
        - fromStudentID: __ID*__ the student id
        - toTutorID: __ID*__ the tutor id
        - startTime: __AWSDateTime*__ the session start at (AWSDateTime format: __YYYY-MM-DDThh:mm:ss.sssZ__ => *1930-01-01T16:00:00-07:00* )
        - endTime: __AWSDateTime*__ the session end at 
        - status: __enum*__ *(pendingAdmin, pendingTutor, pendingStudent, approved, canceled)*
        - receiverUserName: __String__ the receiver user name to give him access
    2. who has access to it and which:
        - the creator of the session has full access
        - the Tutor has full access
        - the admin has full access

4. __testimonial__
    1. Creating the testimonial
        - toUserID: __ID*__
        - fromUserID: __ID*__
        - rating: __AWSJSON*__
        - comment: __String*__
        - receiverUserName: __String*__ the receiver user name to gave him read access
    2. who has access to it and which:
        - the creator of the testimonial has full access
        - the receiver has Read access
        - the admin has full access