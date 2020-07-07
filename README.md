Create Tasks:

oc create -f tasks/s2i-model-task.yaml
oc create -f tasks/openshift-client-task.yaml


Create Pipeline with the tasks we defined earlier
oc create -f pipeline/deploy-model-pipeline

Create Pipeline resources needed
oc create -f resources/git-model-pipeline-resource.yaml
oc create -f resources/image-model-pipeline-resource.yaml

Once the pipeline resources are created, trigger the pipeline using cli or through console
tkn pipeline start deploy-model-pipeline \
-r model-git=chatbot-model-git \
-r model-image=chatbot-model-image \
-s pipeline


After running this command, command, the pipeline you created earlier is now running. Some pods get created to execute the tasks defined as part of the pipeline. After 4-5 minutes, the pipeline run should finish successfully.

To check the success, list pipeline runs
tkn pr ls