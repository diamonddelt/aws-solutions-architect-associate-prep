# AWS OpsWorks

An orchaestration service using `Chef`, the configuration management framework, currently in top standing against other frameworks like Ansible or SaltStack.

Chef uses `recipes` to maintain consistent configuration state of servers.

OpsWorks is a wrapper for chef, so you are still writing the Ruby recipes, only they are stored, validated, managed, and applied with OpsWorks instead you having to manually do this yourself via command line. You also do not need to hook up any of the Chef infrastructure, because OpsWorks does this for you.