# github-actions-experiments
GitHub Actions Experiments

### gh-pages

Create the gh-pages branch, push it to github

    $ git checkout -b gh-pages # not an orphaned branch
    # we don't care, we do not intend to keep its history anyway.
    $ git push --set-upstream origin gh-pages

In the settings, panel, select the gh-pages as the Github pages source 
(now it's quite extensively configurable, I am not sure it's the best
option anymore : the branch & directory can be selected).


**TODO:** configure github-pages actions stuff.