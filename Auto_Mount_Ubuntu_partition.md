# Mount `DevSpace` Partition Automatically in Ubuntu

This guide configures the Ubuntu partition `/dev/nvme0n1p6` (labelled `DevSpace`) to mount automatically at:

```text
/devspace
```

After setup, it can be accessed directly from the terminal with:

```bash
cd /devspace
```

---

## Partition Information

From `lsblk -f`:

| Property | Value |
|---|---|
| Device | `/dev/nvme0n1p6` |
| Filesystem | `ext4` |
| Label | `DevSpace` |
| UUID | `23c9eaf2-156a-4d7c-9df7-47143944f526` |
| New mount point | `/devspace` |

---

## Step 1 — Confirm the Partition

Run:

```bash
lsblk -f
```

Confirm that `/dev/nvme0n1p6` is the `DevSpace` ext4 partition.

---

## Step 2 — Unmount the Existing Mount

The partition is currently mounted at:

```text
/run/media/aditya/DevSpace
```

Unmount it:

```bash
sudo umount /run/media/aditya/DevSpace
```

If you get a "target is busy" error, leave that directory first:

```bash
cd ~
```

Then run the unmount command again.

---

## Step 3 — Create the New Mount Point

Create `/devspace`:

```bash
sudo mkdir -p /devspace
```

---

## Step 4 — Mount the Partition

Mount the partition manually:

```bash
sudo mount /dev/nvme0n1p6 /devspace
```

Check that it is mounted:

```bash
lsblk -f
```

You should see `/devspace` as the mount point for `nvme0n1p6`.

---

## Step 5 — Access the Partition

You can now access it directly:

```bash
cd /devspace
```

List its contents:

```bash
ls -la
```

Check disk usage:

```bash
df -h /devspace
```

---

## Step 6 — Configure Automatic Mounting

Open the filesystem table:

```bash
sudo nano /etc/fstab
```

Add this line at the bottom:

```text
UUID=23c9eaf2-156a-4d7c-9df7-47143944f526 /devspace ext4 defaults 0 2
```

### What this means

- `UUID=23c9eaf2-156a-4d7c-9df7-47143944f526` → identifies the `DevSpace` partition
- `/devspace` → mount point
- `ext4` → filesystem type
- `defaults` → standard mount options
- `0` → disables `dump`
- `2` → filesystem check order after the root filesystem

Save the file:

1. Press `Ctrl + O`
2. Press `Enter`
3. Press `Ctrl + X`

---

## Step 7 — Test `/etc/fstab`

Do **not reboot immediately**. First test the configuration:

```bash
sudo umount /devspace
sudo mount -a
```

If there is no error, the `fstab` entry is valid.

Check:

```bash
lsblk -f
```

You should see:

```text
nvme0n1p6  ext4  DevSpace  23c9eaf2-156a-4d7c-9df7-47143944f526  /devspace
```

---

## Step 8 — Test Access

Run:

```bash
cd /devspace
```

Then:

```bash
pwd
```

Expected:

```text
/devspace
```

You can now use the partition like a normal directory:

```bash
mkdir projects
cd projects
touch test.txt
ls
```

---

## Step 9 — Verify Automatic Mounting After Reboot

Restart Ubuntu:

```bash
sudo reboot
```

After logging in, run:

```bash
lsblk -f
```

Then:

```bash
cd /devspace
```

If it opens successfully, the partition is automatically mounted at boot.

---

## Important Notes

### Do not format the partition

Do **not** run commands such as:

```bash
sudo mkfs.ext4 /dev/nvme0n1p6
```

That would format the partition and can destroy its existing data.

### Use the UUID

The `/etc/fstab` configuration uses the UUID rather than `/dev/nvme0n1p6`. This is preferable because device names can potentially change, while the UUID identifies the filesystem.

### If `/devspace` is owned by root

If you cannot create files inside it as your normal user, check:

```bash
ls -ld /devspace
```

You can make your user the owner with:

```bash
sudo chown -R $USER:$USER /devspace
```

Only do this if you want your current user to have ownership of the entire `DevSpace` filesystem.

---

## Final Configuration

The final setup is:

```text
Partition:    /dev/nvme0n1p6
Label:        DevSpace
Filesystem:   ext4
UUID:         23c9eaf2-156a-4d7c-9df7-47143944f526
Mount point:  /devspace
Auto-mount:   Yes
```

The partition can then be accessed from the terminal with:

```bash
cd /devspace
```
