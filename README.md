# github-actions-experiments
GitHub Actions Experiments

### gh-pages

 1. Create the gh-pages branch, push it to github

        $ git checkout -b gh-pages # not an orphaned branch
        # we don't care, we do not intend to keep its history anyway.
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
