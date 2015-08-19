# <a name="vagrant-and-chef-cookbook"/>Deploying using vagrant and the chef cookbook

The Vagrantfile and chef cookbooks are now maintained in a seperate [repository](https://github.com/elijah/cookbook-huginn)

@elijah is working on splitting the vagrant and chef infrastructure out of the huginn code repository.  It's going to be possible to replace the bits in huginn/deployment are with the skeleton at [@elijah/vagrant-huginn](https://github.com/elijah/cookbook-huginn) - which pulls in the refactored / tests-to-be-added chef cookbook at @elijah/cookbook-huginn

The goal of this work is to make things more manageable, better adhere to best practices from the community, and make it easier to iterate on the supporting infrastructure around huginn without much pain.  Several of the wishlist items from the community were going to require some serious refactoring of cookbook code, or at least a restructuring - so we're trying to get on that path.
