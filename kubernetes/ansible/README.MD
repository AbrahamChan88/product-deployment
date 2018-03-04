## -------- deploy-k8s-manifest -------- 
The following information is to provide other possible supplements to this single playbook.
 
#### Possible pre-tasks:
    - Confirm k8s infrastructure exists and if it does not, exit.
    - Not included in this playbook as it should be taken care of in a previous stage (I.e. pipeline).

#### Variables to define if not declared during execution (user or by pipeline):
    workspace_dir: # set dynamically
    product_url: http://domain.com/(latest)|(stable)|(nightly)|(beta)|(alpha)|(build_version)/filename   #set dynamically;
       Consult with your development team for the release versioning structure.
    k8s_cluster_name : set dynamically
    k8s_cluster_port: set dynamically
    k8s_cluster_token: bc265cd6-d904-45ad-b5de-219ae07ab001 # set dynamically
    certificate_path: # reflect certificate management; May not be required at this stage  

#### Display the downloaded file for troubleshooting.
      - debug:
          msg: "{{ item }}"
        with_file:
          - "{{ k8s_manifest_local }}"

#### Example of k8s manifest:
    The file content can be a list or location of where to obtain deployment files per micro-service.
    Update code to deploy per method choosen; currently a single file.
    /
    Example output of single manifest file containing a list for deployment:
    /
    ---
    product_manifest_list:
      - network_subnet_A-namespace.yaml
      - network_subnet_B-namespace.yaml
      - network_subnet_C-namespace.yaml
      - network_subnet_A-secrets.yaml
      - network_subnet_B-secrets.yaml
      - network_subnet_C-secrets.yaml
      - product_microservice_1-manifest.yaml
      - product_microservice_2-manifest.yaml
      - product_microservice_3-manifest.yaml
      - components_1-manifest.yaml
      - components_2-manifest.yaml
      - components_3-manifest.yaml

#### How to execute code remotely: 
    Example from Ansible documents: 
    - name: Example of looping over a REMOTE command result
      shell: "/usr/bin/something"
      register: command_result

    - name: Do something with each result
      shell: "/usr/bin/something_else --param {{ item }}"
      with_items:
        - "{{ command_result.stdout_lines }}"