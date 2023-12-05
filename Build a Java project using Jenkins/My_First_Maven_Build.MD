# Create a First Maven Jenkins job to build hello-world project 
### Steps
Login to Jenkins console
   Create *Jenkins job -My_First_Maven_Build.

   - Source Code Management:
      - Repository: 'Link to hello-worl project'
      - Branches to build : `*/master`  
   - Build:
     - Root POM:`pom.xml`
     - Goals and options: 'clean install'