
# What Is The Maven Indexer?

The Maven Indexer is a library created by the Apache Maven team which can produce a Lucene Index and carry out queries against it. This compressed index can be used by:
* Artifact repository managers
 * Check if a remote host contains an artifact, class, etc
 * Check what versions of an artifact exist
* IDE-s
 * Resolve dependencies
 * To find out which packages contain the class you would like to import
* Custom tools

# How Does The Maven Indexer Work?

The Maven Indexer scans through `maven-metadata.xml` files and produces a compressed Lucene Index which can be downloaded by consumers.

# What Is The Maven Indexer Used For In The Strongbox Project?

The Maven Indexer is used for integration with IDE-s. Strongbox has it's own internal implementation stored in OrientDB, based on which the Lucene indexes are built.

The Maven indexes produced by most public repository managers (such as Maven Central), are usually rebuilt once a week, as it can take quite a while to scan large repositories with countless small artifacts. Hence, these indexes have proven to not be quite as up-to-date, as the real server's contents. For this reason, we are using OrientDB to keep more accurate information.

# Where Are The Maven Indexes Located?

Every repository has an index under the `strongbox-vault/storages/${storageId}/${repositoryId}/.index` directory where the index is located.

# Do Maven Indexes Break And How To Repair Them?

Usually, you don't need to rebuild the index, because all artifact operations should be handled via the REST API.

However, there are cases like for example:
- Some artifacts have gone missing (hdd error, or somebody removed them and you need to restore one, or a whole batch of them manually directly on the file system without not using the REST API)
- You have added/removed some artifact(s) manually on the file system and would like to update the index

# Information For Developers

The code for the Maven indexing is located under the [strongbox-storage-indexing](https://github.com/strongbox/strongbox/tree/master/strongbox-storage/strongbox-storage-indexing) module.

# See Also
* [Maven Indexer: Github](https://github.com/apache/maven-indexer/)
* [Maven Indexer: About](http://maven.apache.org/maven-indexer-archives/maven-indexer-LATEST/index.html)
* [Maven Indexer: Fields](http://maven.apache.org/maven-indexer-archives/maven-indexer-LATEST/indexer-core/index.html)
* [Maven Indexer: Examples](https://github.com/apache/maven-indexer/tree/master/indexer-examples)
* [Maven Metadata](https://github.com/strongbox/strongbox/wiki/Maven-Metadata)