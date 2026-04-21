pipeline {
    agent any
    stages {
        stage('Debug branch') {
            steps {
                echo "BRANCH_NAME=${env.BRANCH_NAME}"
                echo "CHANGE_ID=${env.CHANGE_ID}"
                echo "GIT_BRANCH=${env.GIT_BRANCH}"
            }
        }
        stage("BlackDuckSecruityScan") {
            when {
                // Triggering Black Duck Security Scan on master branch or Pull Request
                anyOf {
                    branch 'master'
                    branch pattern: "PR-\\d+", comparator: "REGEXP"
                }
            }
            steps {
                echo 'BLACK DUCK SECURITY SCAN - POLARIS STARTED'
                script {    
                       //security_scan product: "polaris", 
                       security_scan product: "blackducksca",
                           // Fix pull request creation
                        // blackducksca_fixpr_enabled: true,
                        // blackducksca_fixpr_filter_severities : "CRITICAL, MEDIUM",
                        // blackducksca_fixpr_maxCount: 1
                      // Uncomment if below parameters are not set in global configuration
                         polaris_server_url: 'POLARIS_SERVER_URL',
                         polaris_access_token: 'POLARIS_TOKEN',
                      // bitbucket_token: 'BITBUCKET_TOKEN', // Used for PR comment. Use github_token for GitHub or gitlab_token for GitLab
                      // bitbucket_username:'BITBUCKET_USERNAME' // Used for bitbucket cloud pr comment if app password is set as bitbucket_token 
                         // polaris_assessment_types: 'SCA,SAST',
                          polaris_fixpr_enabled: true,
                         // polaris_fixpr_useUpgradeGuidance: 'SHORT_TERM',
                           polaris_fixpr_maxCount: 3,
                           //polaris_fixpr_filter_severities: 'CRITICAL',
                      //Optional for multibranch pipeline
                      // polaris_application_name: 'POLARIS_APPLICATION_NAME', 
                      // polaris_project_name: 'POLARIS_PROJECT_NAME',
                      // polaris_branch_name: 'BRANCH_NAME',
                       //polaris_waitForScan: false    // Used to support the async mode
                      // project_directory: "PROJECT_DIRECTORY",
                      // Uncomment this to use Source Upload method. Default value is hybrid (build based)
                       //polaris_test_sast_location: 'hybrid'
                       //polaris_test_sca_location: 'remote'
                      // project_source_archive: "PROJECT_SOURCE_ARCHIVE",
                      // project_source_excludes: "PROJECT_SOURCE_EXCLUDES",
                      // project_source_preserveSymLinks: "PROJECT_SOURCE_PRESERVESYMLINKS",
                      // Uncomment this to use Local Analysis feature
                      // Please use Local Analysis or Source Upload exclusively
                      // polaris_test_sast_location: 'local',
                      // Pull Request Comments
                      //  polaris_prComment_enabled: true
                      // polaris_branch_parent_name: 'PARENT_BRANCH_NAME',
                      // SARIF report generation
                      // polaris_reports_sarif_create: true,
                      // Optional parameters
                      // polaris_reports_sarif_file_path: 'SARIF_FILE_PATH',
                      // polaris_reports_sarif_groupSCAIssues: true,
                      // polaris_reports_sarif_issue_types: 'SAST, SCA',
                      // polaris_reports_sarif_severities: 'CRITICAL,HIGH',
                      // Signature scan
                      // polaris_test_sca_type:'SCA-SIGNATURE'
                      // Sigma Rapid scan
                      // polaris_test_sast_type: "SAST_RAPID",
                      // Uncomment below to add arbitrary CL parameters
                      // detect_search_depth: 1,
                      // detect_config_path: '/USER/application.properties',
                      // detect_args: '--detect.diagnostic=true',
                      // coverity_build_command: 'mvn clean install',
                      // coverity_clean_command: 'mvn clean',
                      // coverity_config_path: '/USER/coverity.yml',
                      // coverity_args: '--config-override capture.build.build-command=mvn install',
                      // coverity_version: '2025.9.0',
                      // Mark build status if issues found
                      //  mark_build_status: 'UNSTABLE'
                   // Uncomment to add custom logic based on return status
                  // if (status == 8) { unstable 'policy violation' }
                  // else if (status != 0) { error 'plugin failure' }
                }
            }
        }
    }
}