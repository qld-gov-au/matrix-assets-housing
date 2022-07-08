# matrix-assets-boilerplate

This repository provides a boilerplate for you to fork to create franchise specific assets used by qld.gov.au Squiz Matrix CMS and connects to matrix via Git bridge.

All JS and CSS assets in this repository will be compressed, minified or bundled and serve to the binary repository.
Then the end user could use Git bridge to synchronise the assets to Squiz Matrix from the binary repository.

All files in the `src` folder will be copied to the binary repository in the same folder structure, as well as they will be compressed and minified.

To bundle the files you could follow the instructions below.

Each time you push or merge the branch, the building process will be triggered by the Github Action and automatically deployed to the binary repository [`matrix-assets-release`](https://github.com/qld-gov-au/matrix-assets-release).

## Folder structure
- src/css : Contains all scss partials related
- src/js: Contains all script files
- binary-repo: files that will be copied to the binary repository, such as the README file of that repository.

## Git bridge branches
- you could git bridge a feature branch for testing changes
- `main` branch is used for production

## Bundling

This repository enable you to bundled a bunch of JS/CSS files and output a single minified bundled file.

There is no limitation of what you want to bundle in this repository:
- You could create as many bundle files as you like in this repository.
- You could choose whatever files you want to add to the bundle.

### Create a bundle

1. Defined a target item in the  `targets` object in `package.json`. Such as:
    ```json
      "targets": {
        "main":false,
        "new-bundle": {
          "source": "src/New Bundle/index.js", // input file location
        }
      },
      "new-bundle": "dist/build/new-bundle.js" // output file location
    ```
2. Create a index file in `src/New Bundle/index.js`.
3. In the index file, import all the asset files you want to bundle. Such as:
    ```js
      import "./js/script1.js";
      import "./js/script2.js";
      import "./js/script3.js";
      import "./css/style1.scss";
      import "./css/style2.scss";
    ```
4. You could test the building process by running `npm run build`, you could see the bundled files will be output to the `distDir`, in `dist/build` it will contain:
    ```
      my-bundle.js
      my-bundle.js.map
      my-bundle.css
      my-bundle.map
    ```
5. Each time you push or merge the branch, the building process will be triggered by the Github Action and automatically deployed to the binary repository.
6. Then you could use Git bridge to synchronise the update in the binary repository to Squiz Matrix from the branch you are working on.

## To fork this repository for a new franchise

You could fork this repository to contain franchise specific assets.

1. Go to https://github.com/qld-gov-au/matrix-assets-boilerplate and click the `fork` button.
2. In `Create a new fork` page, set `Owner` to `qld-gov-au`, you'll need the access of this organisation.
3. You could set whatever in `Repository name`, such as `matrix-assets-housing`.
4. You could set whatever in `Description`.
5. Then press `Create fork` to create a new repository.
6. In the new repository, go to `Settings` > `Secrets` > `Actions`.
7. For details of the following steps, please refer to `.github/workflows/README.md`
8. Add a `New repository secret`.
9. Set the name as `TARGET_REPO`, for the value, it will be the name of the new binary repository you are going to created, such as `qld-gov-au/matrix-assets-housing-release`. Save this secret.
10. Add another `New repository secret`.
11. Set the name as `GH_PAT`, for the value, it will be something like this: `YourGithubUsername:YourPersonalAccessToken`
12. Follow this [guide](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) for getting `YourPersonalAccessToken`. You'll only need to enable the `Repo` access right for this token, and you could save this token in 1Password for future usage.
13. Create a new binary repository in https://github.com/organizations/qld-gov-au/repositories/new
14. Use the binary repo name you've defined previously, eg. `matrix-assets-housing-release`, and check `Add a READMEfile`. Then submit.
15. Now you've setup both franchise repository and binary repository, every push in the source repository will automatically build and publish to the binary repository. You could synchronise the binary repository inn Squiz Matrix Gitbridge now.



