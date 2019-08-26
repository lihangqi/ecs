# Limits {#concept_jzp_qtd_zdb .concept}

You can bind tags to the following resources in the ECS console: ECS instance, storage, snapshot, image, and security group.

Tags have the following limits:

-   Each tag has a key-value pair.
-   You can bind 20 tags to an instance at most. You can bind 20 tags at most to an instance at a time.
-   Every tag key of a resource must be unique. A tag with the same key as an existing one will be overwritten.
-   Tag information is not shared across regions. For example, tags created in China East 1 \(Hangzhou\) are invisible to China East 2 \(Shanghai\).
-   If a tag is unbound and no longer bound to any other resource, the tag will be automatically deleted.

