# How to submit your project

To submit your project it is required that you create a new release using **Github Releases**.  
This will be used to know the exact version that will be assessed.

## Make Sure Your App is Tested and the Repository is Up to Date

Your github repository should have a working application runnable through Docker
and have the latest commit that needs to be evaluated.  
To ensure this, use the following commands

```shell
# run the application with Docker
docker build <Dockerfile_directory> -t app:tag
docker run app:tag [options needed ...]

# ensure the latest version is committed
git commit -m "...comment..."
git push 
```

This last commit must then be tagged with the tag \`final\`, which creation will be shown later.

## Creation of a tag with Git command line

A **tag** created using the Git command line needs to then be pushed to the repository.  
This can be done by using the following commands:

```shell
# add the 'final' tag and push it
git tag final
git push origin --tags
```

After its creation, it is recommended to create a new release to make it easily accessible.

Important: the tag name to be submitted is **final**, all lowercase, no quotes, no whitespaces, no other characters, and it must be associated with the commit to be evaluated.

## Creation of the Release with Github interface

1. Go to the repository on GitHub.  
2. Click on **Create a new Release** in the **Releases** tab (on the right-hand side, below the repo description).
<img src="../image/image2.png" alt="Create new Release"  />
3. Fill out the release information <img src="../image/image2.png" alt="Release info"  />
4. Select the tag **final** from which the release will be created (click on **Create new tag** if it wasn’t created from the command line)<img src="../image/image1.png" alt="Select tag"  />
5. The release form should look like this <img src="../image/image4.png" alt="Release information"  />
6. Click on **Publish release** to finish the creation and submit for assessment<img src="../image/image5.png" alt="Publish release"  />
