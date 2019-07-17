gitlab CI/CD Note
================

.gitlab-ci.yml
--------------
Create a .gitlab-ci.yml config in the  root  of your repository. 
    
    > touch .gitlab-ci.yml
    > vi .gitlab-ci.yml
    
    # node express config  
    image: node:10
    before_script:
    - npm install
    - npm audit fix
    
    test:
    script:
    - npm test


Docker
--------------
Run gitlab runner in a container.

    > #centOS
    > yum install docker-ce
    > docker run -d --name gitlab-runner --restart always -v /var/run/docker.sock:/var/run/docker.sock -v /srv/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner:latest
    
    # Check process
    > docker ps
    > docker exec -it gitlab-runner gitlab-runner register 

    coordinator URL and token is in the gitlab project CI/CD setting / runner
    you can choose  Runners activated for this project in the same page.

Mocha 
--------------
1. It is a testing framework of javascipt.

2. Here is the example for testing express.
    ```
    # server_test.js
    var request = require("supertest");
    var server = require("./app.js");
    var assert = require("assert");
    it("statusCode should return 200", function(done)
    {
        request(server)
            .get("/")
            .expect(200)
            .expect(function(res)
            {
                assert.equal(res.statusCode, 200);
            })
            .end(done);
    });
    ```
        > mocha server_test.js 
        # Add this code to the package.json and it will auto testing your server status after you psuh your code to gitlab.
