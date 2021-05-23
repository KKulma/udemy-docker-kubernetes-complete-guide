### our single-container workflow

GH push 
--> Travis pulls images
            tests images
            tests code
            pushes code to AWS EB
--> AWS EB pulls images 
            builds images 
            deploys

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
