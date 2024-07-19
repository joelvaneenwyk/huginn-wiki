Follow these instructions if you wish to add private features to your version of Huginn. GitHub doesn't make it easy to work with private forks of public repositories, so I recommend that you follow the following steps:

- Make a private, empty GitHub repository called `huginn-private` and duplicate your public Huginn fork into your new private repository (via [GitHub's instructions](https://help.github.com/articles/duplicating-a-repository)):

        git clone --bare git@github.com:you/huginn.git
        cd huginn.git
        git push --mirror git@github.com:you/huginn-private.git
        cd .. && rm -rf huginn.git

- Checkout your new private repository.
- Add your Huginn public fork as a remote to your new private repository (`huginn-private`):

        git remote add public git@github.com:you/huginn.git

- Run the steps from [_Quick Start_](https://github.com/cantino/huginn#quick-start) in the README to configure your copy of Huginn.
- When you want to contribute patches, do a remote push from your private repository to your public fork of the relevant commits, then make a pull request to this repository.
