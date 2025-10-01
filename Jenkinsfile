pipeline {

    agent any

    environment {

        GXServerCredentials = "GXServer18"

        /* Stage 'Build KB' */

        MSBuildPath = "C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\BuildTools\\MSBuild\\Current\\Bin"
        GeneXusInstallationPath = "C:\\Program Files (x86)\\GeneXus\\GeneXus18U13" 
        LocalKBPath = "C:\\Models\\LetsPlai"
        LocalKBVersion = 'LetsPlai'
        LocalKBEnvironment = 'DEV'
        ForceRebuild = 'false'
        CompileMains = 'true'

        buildMSBuildScript = '"%MSBuildPath%\\MSBuild.exe" "%GeneXusInstallationPath%\\TeamDev.msbuild" ' +
                             '/p:DbaseServerUsername="local\\root" ' +
                             '/p:DbaseServerPassword="root" ' +
                            //  '/p:DbaseServerUsername="%GXServerUsername%" ' +
                            //  '/p:DbaseServerPassword="%GXServerPassword%" ' +
                             '/p:WorkingDirectory="%LocalKBPath%" ' +
                             '/p:WorkingVersion="%LocalKBVersion%" ' +
                             '/p:WorkingEnvironment="%LocalKBEnvironment%" ' +
                             '/p:ForceRebuild="%ForceRebuild%" ' + 
                             '/p:CompileMains="%CompileMains%" ' +
                             '/t:Build'

        /* Stage 'Run GXRecorder Tests' */

        TestType = 'UI'

        runGXRecorderTestsScript = '"%MSBuildPath%\\msbuild.exe" "%GeneXusInstallationPath%\\RunAllTests.msbuild" ' +
                                   '/p:GX_PROGRAM_DIR="%GeneXusInstallationPath%" ' +
                                   '/p:KBPath="%LocalKBPath%" ' +
                                   '/p:EnvironmentName="%LocalKBEnvironment%" ' +
                                   '/p:TestType="%TestType%" ' +
                                   '/p:GXUser="%GXServerUsername%" ' +
                                   '/p:GXPass="%GXServerPassword%" ' +
                                   '/t:RunAllTests'

    }

    stages {

        // stage('Build KB') {

        //     steps {

        //         echo 'Start Build KB'

        //         script {

        //             withCredentials([usernamePassword(credentialsId: "${env.GXServerCredentials}", passwordVariable: 'GXServerPassword', usernameVariable: 'GXServerUsername')]) {

        //                 bat label: 'Build KB MSBuild Script',
        //                 script: "${env.buildMSBuildScript}"

        //             }

        //         }

        //         echo 'End Build KB'

        //     }

        // }

            
        stage('Run GXRecorder Tests') {

            steps {

                echo "Start Run GXRecorder Tests"

                script {

                    withCredentials([usernamePassword(credentialsId: "${env.GXServerCredentials}", usernameVariable: 'GXServerUsername', passwordVariable: 'GXServerPassword')]) {

                        bat label: "Run GXRecorder Tests",
                        script: "${env.runGXRecorderTestsScript}"

                    }

                }

                echo "End Run GXRecorder Tests"

            }

        }

    }                   

}
