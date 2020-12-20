

# github-actions-experiments
GitHub Actions Experiments

[![main](https://github.com/boisgera/github-actions-experiments/workflows/main/badge.svg)](https://github.com/boisgera/github-actions-experiments/actions)

### conda environments

First, before the job steps:

    defaults:
      run:
        shell: bash -l {0}    

then

    - uses: conda-incubator/setup-miniconda@v2
      with:
        activate-environment: CDIS
        environment-file: environment.yml

### gh-pages

There are at least two widely used actions for gh-pages deployments:

  - <https://github.com/marketplace/actions/deploy-to-github-pages> (1.2k)

  - <https://github.com/peaceiris/actions-gh-pages> (1.5k)

So far I have been able to only make the first work (the second one not at all), 
but only with non-orphaned gh-pages branch, like that:

 1. Create the (non-orphaned) gh-pages branch, push it to github

        $ git checkout -b gh-pages 
        $ git push --set-upstream origin gh-pages

 2. In the settings, panel, select the gh-pages as the Github pages source 
    (now it's quite extensively configurable, I am not sure it's the best
    option anymore : the branch & directory can be selected).

 3. Configure github-pages actions stuff:

        - name: deploy to gh-pages
          uses: JamesIves/github-pages-deploy-action@3.7.1
          with:
            GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
            BRANCH: gh-pages
            FOLDER: "."
            SINGLE_COMMIT: true

Now, if I kill this branch and update this deletion remotely : 

    $ git branch -d gh-pages
    $ git push origin --delete gh-pages

Oh wow, the github actions RECREATES the gh-pages branch. Isn't that nice?
OK, so that's not the issue. The issue is with the `.gitignore` file ; nothing
that is ignore by this file will be deployed AND deleting the file 
(or overlay something) before the deployment won't work. How annoying is that? 
Very. But at least the issue is well identified.

OK, well, the `PRESERVE: false` option seem to be solving it.
