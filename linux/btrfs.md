# Btrfs

Btrfs, also known as the B-tree filesystem, is a copy-on-write (CoW) filesystem for Linux. It was initially developed by Oracle for use in Linux and was first introduced in the 2.6.29 kernel. It is now a part of the mainline Linux kernel and is actively developed by a community of developers.

Btrfs includes several advanced features that make it a powerful and flexible filesystem for Linux. Some of the key features include:

## Pooling

With Btrfs pooling, users can add or remove storage devices to the pool dynamically, without needing to worry about partitioning or managing multiple filesystems. This makes it easy to scale storage as needed, without having to worry about the underlying storage configuration.

Btrfs pooling works by using a concept called a "subvolume", which is a logical partition within the Btrfs filesystem. Subvolumes can be used to organize and manage data within the filesystem, and they can be created and resized dynamically.

When multiple physical devices are added to the Btrfs pool, the filesystem uses a technique called striping to spread data across the devices. This provides increased performance and capacity, as data can be read and written from multiple devices simultaneously.

Btrfs pooling also includes support for redundancy, which is achieved through techniques such as mirroring and RAID. By storing redundant copies of data on separate devices, Btrfs can provide increased fault tolerance and protection against data loss.

## Snapshots

Btrfs snapshots are a key feature of the Btrfs filesystem that allows users to create point-in-time copies of the filesystem. Snapshots are read-only, so they cannot be modified, but they can be used to create new subvolumes or to restore the filesystem to a previous state.

Btrfs snapshots work by creating a copy-on-write (CoW) clone of the filesystem. When a snapshot is created, any changes made to the filesystem are written to a new location, rather than overwriting the original data. This ensures that the original data remains unchanged, even if the snapshot is modified or deleted.

Snapshots can be created quickly and efficiently, and they use a minimal amount of disk space, as they only store the changes that have been made to the filesystem since the snapshot was created. This makes them a powerful tool for backup, recovery, and testing.

Btrfs snapshots can be created manually, or they can be created automatically on a regular schedule, such as daily or weekly. This allows users to maintain multiple snapshots of the filesystem, which can be used to restore the system to a previous state in the event of data loss or corruption.

In addition to full snapshots, Btrfs also supports incremental snapshots, which allow users to create snapshots that only contain the changes that have been made since a previous snapshot. This can be useful for creating backups that are more efficient and take up less disk space.

## Checksums

Btrfs uses checksums to ensure data integrity and detect data corruption. Each block of data on the filesystem is assigned a unique checksum, which is generated using a cryptographic hash function. When data is read from the filesystem, the checksum is computed again and compared to the original checksum. If the two checksums do not match, it is assumed that the data has been corrupted and the system can take corrective action.

Btrfs uses checksums to provide data integrity and reliability for all data stored on the filesystem, including user data, metadata, and file system structures. The use of checksums allows Btrfs to detect and automatically repair data corruption, even if it occurs in a redundant copy of the data.

Btrfs uses different checksum algorithms depending on the version and configuration of the filesystem. The default checksum algorithm is CRC32c, which is a fast and efficient checksum algorithm that is widely used in networking and storage applications. Btrfs also supports other checksum algorithms, such as SHA-256 and SHA-512, which are more secure but slower to compute.

In addition to checksums, Btrfs also supports data scrubbing, which is a process that reads all of the data on the filesystem and verifies its integrity using checksums. Data scrubbing is typically performed on a regular schedule, such as weekly or monthly, and it can be used to detect and correct data corruption before it causes problems.

## Multi-device spanning

Multi-device spanning is a key feature of the Btrfs filesystem that allows users to span a single filesystem across multiple physical devices, providing increased performance and reliability. With multi-device spanning, users can combine multiple storage devices into a single logical volume, which can be used to store large amounts of data.

When multiple devices are added to the Btrfs pool, the filesystem uses a technique called striping to spread data across the devices. This provides increased performance and capacity, as data can be read and written from multiple devices simultaneously. If one device fails, the data can still be accessed from the remaining devices, providing increased fault tolerance and protection against data loss.

Btrfs supports several different striping modes, including RAID0, RAID1, and RAID10. RAID0 striping provides the best performance, but offers no redundancy or fault tolerance. RAID1 striping provides redundancy by storing multiple copies of data on separate devices, while RAID10 provides a combination of striping and mirroring for increased performance and redundancy.

In addition to striping, Btrfs also supports other advanced features that make it a powerful and flexible filesystem for multi-device spanning. For example, Btrfs can detect and automatically repair data corruption using checksums, and it supports efficient and flexible snapshotting for backup and recovery.

## Online defragmentation

Btrfs includes a built-in defragmentation tool that can defragment the filesystem while it is in use, without requiring downtime or unmounting the filesystem.

