node('master') {
    checkout scm

    dir('chef-repo'){

        stage('Get Chef Repo'){
                        
            git 'https://github.com/devopsevd/chef_docker_cookbooks.git'

        }
        
        stage('Check Knife cookbook'){
                        
            if (isUnix()) {
                sh "knife cookbook list"
            } else {
                bat(/knife cookbook list/)
            }

        }    

        stage('Check Knife vsphere'){
                        
            if (isUnix()) {
                sh "knife vsphere template list"
            } else {
                bat(/knife vsphere template list/)
            }

        }      

                
         stage('Creat VM') {

             if (isUnix()) {
                 sh "knife vsphere vm clone chefAutoMat152 --template CentOsTemplate --start true --node-name chefAutoMat152 --resource-pool 'Compute/Chef_Test' --cspec CentOs_Chef --cips 10.118.40.152/24 --cdomain csa.local --verbose"
             } else {
                 bat(/knife vsphere vm clone chefAutoMat152 --template CentOsTemplate --start true --node-name chefAutoMat152 --resource-pool "Compute\/\Chef_Test" --cspec CentOs_Chef --cips 10.118.40.152\/\24 --cdomain csa.local --verbose/)
             }
         }
        
        
        stage('Add VM as chef node') {

             if (isUnix()) {
                 sh "knife bootstrap 10.118.40.152 --ssh-user root --ssh-password Password1 --node-name chefAutoMat152 --sudo --verbose"
             } else {
                 bat(/knife bootstrap 10.118.40.152 --ssh-user root --ssh-password Password1 --node-name chefAutoMat152 --sudo --verbose/)
             }
         }

        // stage('Install docker on VM') {

        //     stage('Add recipe') {
    
        //         if (isUnix()) {
        //             sh "knife node run_list add chefAutoMat241 'role[dockerinstall]'"
        //         } else {
        //             bat(/knife node run_list add chefAutoMat241 'role[dockerinstall]'/)
        //         }
        //     }
        //     stage('run recipe on node') {
    
        //         if (isUnix()) {
        //             sh "knife ssh 'name:chefAutoMat241' 'sudo chef-client' -a ipaddress --ssh-user root --ssh-password Password1 --verbose"
        //         } else {
        //             bat(/knife ssh 'name:chefAutoMat241' 'sudo chef-client' -a ipaddress --ssh-user root --ssh-password Password1 --verbose/)
        //         }
        //     }
        //     stage('Remove recipe') {
    
        //         if (isUnix()) {
        //             sh "knife node run_list remove chefAutoMat241 'role[dockerinstall]'"
        //         } else {
        //             bat(/knife node run_list remove chefAutoMat241 'role[dockerinstall]'/)
        //         }
        //     }
        // }
        // stage('Pull and run container') {

        //     stage('Add recipe') {
    
        //         if (isUnix()) {
        //             sh "knife node run_list add chefAutoMat241 'role[dockerrun]'"
        //         } else {
        //             bat(/knife node run_list add chefAutoMat241 'role[dockerrun]'/)
        //         }
        //     }
        //     stage('run recipe on node') {
    
        //         if (isUnix()) {
        //             sh "knife ssh 'name:chefAutoMat241' 'sudo chef-client' -a ipaddress --ssh-user root --ssh-password Password1 --verbose"
        //         } else {
        //             bat(/knife ssh 'name:chefAutoMat241' 'sudo chef-client' -a ipaddress --ssh-user root --ssh-password Password1 --verbose/)
        //         }
        //     }
        //     stage('Remove recipe') {
    
        //         if (isUnix()) {
        //             sh "knife node run_list remove chefAutoMat241 'role[dockerrun]'"
        //         } else {
        //             bat(/knife node run_list remove chefAutoMat241 'role[dockerrun]'/)
        //         }
        //     }
        // }

    }
}
