pipeline
{

    agent any

    environment {

        MSBuildPath = "C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\BuildTools\\MSBuild\\Current\\Bin"
        GeneXusInstallationPath = "C:\\Program Files (x86)\\GeneXus\\GeneXus18U12"       
        LocalKBPath = "C:\\Models\\CONUAR_Requerimientos"
        LocalKBEnvironment = "DEV"
        TestType = 'UI'
        GXRecorderTestsFilePath = "E:\\Jenkins_root\\workspace\\BANCOR\\BancorTrunk\\Tests"

        GXServerCredentials = "GXServer18"

        runGXRecorderTestsScript = '"%MSBuildPath%\\msbuild.exe" "msbuild\\RunAllTests.msbuild" ' +
                                   '/p:GX_PROGRAM_DIR="%GeneXusInstallationPath%" ' +
                                   '/p:KBPath="%LocalKBPath%" ' +
                                   '/p:EnvironmentName="%LocalKBEnvironment%" ' +
                                   '/p:TestType="%TestType%" ' +
                                   '/p:GXServerUser="%GXServerUsername%" ' +
                                   '/p:GXServerPass="%GXServerPassword%" ' +
                                //    '/p:JUnitTestFilePath="%GXRecorderTestsFilePath%" ' +
                                   '/t:RunAllTests'

    }

    stages {
            
        stage("Run GXRecorder Tests") {

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
