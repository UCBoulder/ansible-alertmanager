New roles should be initialized using the existing skeletons structure, this will provide you with sensible defaults and remove some files that simply are not used inside of a collection.

Example:

    roles/ $ ansible-galaxy role init --role-skeleton ../skeletons/role/ your-role-name-here

You will still need to update the meta/main.yml file located in the newly created role, defaults have been provided, but more work is necessary.