
```javascript

name: Automerge my-pages to main
on:
   push:
    branches:    
      - my-pages
      
 jobs:
  automerge:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Merge my-pages to main
        if: github.event.pull_request.merged == true
        uses: actions/github-script@v6
        with:
          script: |
            const github = require('@actions/github');
            const core = require('@actions/core');

            const context = github.context;
            const octokit = github.getOctokit(core.getInput('token'));

            await octokit.rest.pulls.create({
              owner: context.repo.owner,
              repo: context.repo.repo,
              head: 'my-pages',
              base: 'main',
              title: `Merge my-pages to main`,
            });
```
