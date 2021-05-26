### our single-container workflow

GH push 
--> Travis pulls images
            tests images
            tests code
            pushes code to AWS EB
--> AWS EB pulls images 
            builds images 
            deploys


AWS EB, if there's a single Dockerfile, builds it by default. In the multi-container scenario we need to configure these builds in `Dockerrun.aws.json`.
### our multi-container workflow

GH push 
--> Travis pulls images
            tests images
            tests code
            builds prod images
            pushes images to container repository
            pushes project to AWS EB
--> AWS EB pulls images 
            deploys

Advantages of the multi-container workflow: images are built only ones and their built is independent of the AWS EB
