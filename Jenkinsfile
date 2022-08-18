#!/usr/bin/groovy
// Declarative Pipeline
@Library('shared-lib') 
import jenkinslib.JenkinsSharedLibUtil
import static util.Utilities.*
import util.*
def jenkinsSharedLibUtil = new JenkinsSharedLibUtil()
def utils2 = new Utilities2(this)
pipeline {
	agent any

	stages {
		stage("shared lib demo") {
            steps {
                //since jenkinsSharedLibUtil is Java/Groovy class, so they're inside script tag
                script {
                    def s1 = jenkinsSharedLibUtil.sayHi()
                    def s2 = jenkinsSharedLibUtil.sayHi2()
                    println "s1=${s1}"
                    println "s2=${s2}"
					
					mvn (this, 'clean package')
					
					utils2.mvn 'clean package 2'
                }
                //global variables function   

                //takes parameters def call(String name, String dayOfWeek)
                helloWorldSimple("john", "Monday") 

                //pass a Map of name/val to helloWorld
                helloWorld("name": "Doe", "dayOfWeek": "Tues")

                //1. pass map of name/val to helloWorldExternal
                //2. helloWorldExternal.groovy calls loadLinuxScript(name: 'hello-world.sh') to read hello-world.sh and save it
                //3. then run hello-world.sh on the Agent
                helloWorldExternal("name": "Tom", "dayOfWeek": "Wed")
				
				
            }
        }
		
		stage('Build') {
			steps {
				echo 'Building..'
			}
		}

		stage('Test') {
			steps {
				echo 'Testing..'
			}
		}

		stage('Deploy') {
			steps {
				echo 'Deploying....'
			}
		}

	}
}
