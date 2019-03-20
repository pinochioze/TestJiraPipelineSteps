#!/usr/bin/env groovy
node {
  stage('JIRA') {
    checkout scm
    sh '''#!/bin/bash
            echo "hello world - testing jenkins integration for jira"
            whoami
            pwd
            ls -atl .
         '''

    
    println '===================== GET SERVER INFO ====================================================='
    withEnv(['JIRA_SITE=JiraLocal']) {
      def serverInfo = jiraGetServerInfo()
      echo serverInfo.data.toString()
    }


    println '===================== GET INFO from SOF-6 issue  =========================================='
    def issue_sof6 = jiraGetIssue idOrKey: 'SOF-6', site: 'JiraLocal'
    echo issue_sof6.data.toString()


    println '===================== EDIT DESCRIPT on SOF-6 issue  ======================================='
    def testIssue = [fields: [ project: [id: '10000'],
                           summary: 'New JIRA Created from Jenkins.',
                           description: '||No||PR||Commit||UnitTest||FunctionTest||PerfTest||Note||\n|l|PR-1|abcdefghijklm|Passed|Passed|Passed| |\n|2|PR-2|abcdefghijklm|Passed|Passed|Passed| |\n|3|PR-3|abcdefghijklm|Passed|Passed|Passed| |'
                           ]]
    response = jiraEditIssue idOrKey: 'SOF-6', issue: testIssue, site: 'JiraLocal'

    println '===================== ADD COMMENTS IN SOF-6  ============================================'
    comment = [ body: 'There is new commit on GitHub' ]
    jiraAddComment site: 'JiraLocal', idOrKey: 'SOF-6', input: comment
    
    println '===================== EDIT COMMENTS IN   ================================================'
    comment = [ body: '||No||PR||Commit||UnitTest||FunctionTest||PerfTest||Note||\n|l|PR-10|qwertyuiopasd|Passed|Passed|Passed| |\n|2|PR-20|abcdefghijklm|Passed|Passed|Passed| |\n|3|PR-30|abcdefghijklm|Passed|Passed|Passed| |' ]
    jiraEditComment site: 'JiraLocal', idOrKey: 'SOF-6', commentId: '10007', input: comment

    println '===================== GET COMMENT IN SOF-6  =============================================='
    def comment = jiraGetComment site: 'JiraLocal', idOrKey: 'SOF-6', commentId: '10007'
    echo comment.data.toString()
    

    println '===================== GET ALL COMMENTS IN SOF-6  ========================================='
    def comments = jiraGetComments site: 'JiraLocal', idOrKey: 'SOF-6'
    echo comments.data.toString()

    println '===================== UPLOAD ATTACHMENT IN SOF-6  =========================================='
    def attachment = jiraUploadAttachment idOrKey: 'SOF-6', file: 'TestingReport4JiraSteps.csv', site: 'JiraLocal'
    echo attachment.data.toString()

 }
}
