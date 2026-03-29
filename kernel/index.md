---
layout: default
title: Kernel Patches
---

<p>
  Patches merged into the mainline Linux kernel. Bugs primarily sourced from
  <a href="https://syzkaller.appspot.com" target="_blank">syzbot</a> and fixed
  across filesystems, memory management, networking, and core kernel subsystems.
</p>

<h2 id="fork">kernel/fork</h2>

<ul class="item-list">
  <li>
    <div class="item-subsystem">Mar 2026</div>
    <div>
      <div><strong>validate exit_signal in kernel_clone()</strong></div>
      <div class="item-meta">
        Fixed invalid exit_signal values (65–255) silently accepted by clone() syscall.
        Moved check from syscall handler to kernel_clone() to cover all callers including
        sys_ia32_clone(). Reviewed-by: Oleg Nesterov. Signed-off: Andrew Morton.
      </div>
      <div class="item-links">
        <a href="https://lkml.kernel.org/r/20260316151956.563558-1-kartikey406@gmail.com" target="_blank">LKML</a>
        <a href="https://lore.kernel.org/all/20260316151956.563558-1-kartikey406@gmail.com/" target="_blank">lore.kernel.org</a>
        <a href="https://syzkaller.appspot.com/bug?extid=bbe6b99feefc3a0842de" target="_blank">syzbot</a>
      </div>
    </div>
  </li>
</ul>

<h2 id="ext4">ext4</h2>

<ul class="item-list">
  <li>
    <div class="item-subsystem">Feb 2026</div>
    <div>
      <div><strong>convert inline data to extents when truncate exceeds inline size</strong></div>
      <div class="item-meta">
        Fixed a kernel BUG_ON() triggered when truncate() grows a file with INLINE_DATA
        flag beyond inline capacity (~60 bytes), then sendfile() attempts a write.
        Added conversion to extent-based storage in ext4_setattr(). Signed-off: Theodore Ts'o.
      </div>
      <div class="item-links">
        <a href="https://patch.msgid.link/20260207043607.1175976-1-kartikey406@gmail.com" target="_blank">patch</a>
        <a href="https://syzkaller.appspot.com/bug?extid=7de5fe447862fc37576f" target="_blank">syzbot</a>
      </div>
    </div>
  </li>
  <li>
    <div class="item-subsystem">Sep 2025</div>
    <div>
      <div><strong>detect invalid INLINE_DATA + EXTENTS flag combination</strong></div>
      <div class="item-meta">
        syzbot reported a BUG_ON in ext4_es_cache_extent() on corrupted filesystems
        with both INLINE_DATA and EXTENTS flags set. Added early detection in ext4_iget()
        to reject the invalid inode with EFSCORRUPTED. Reviewed-by: Zhang Yi. Signed-off: Theodore Ts'o.
      </div>
      <div class="item-links">
        <a href="https://lore.kernel.org/all/20250930112810.315095-1-kartikey406@gmail.com/" target="_blank">lore.kernel.org</a>
        <a href="https://syzkaller.appspot.com/bug?extid=038b7bf43423e132b308" target="_blank">syzbot</a>
      </div>
    </div>
  </li>
  <li>
    <div class="item-subsystem">Sep 2025</div>
    <div>
      <div><strong>validate ea_ino and size in check_xattrs</strong></div>
      <div class="item-meta">
        Added validation in check_xattrs() to detect xattr entries where e_value_size
        is zero but e_value_inum is non-zero, indicating corrupted xattr data.
        Suggested-by: Theodore Ts'o. Signed-off: Theodore Ts'o.
      </div>
      <div class="item-links">
        <a href="https://lore.kernel.org/all/20250923133245.1091761-1-kartikey406@gmail.com/" target="_blank">lore.kernel.org</a>
        <a href="https://syzkaller.appspot.com/bug?extid=4c9d23743a2409b80293" target="_blank">syzbot</a>
      </div>
    </div>
  </li>
</ul>

<h2 id="ntfs3">fs/ntfs3</h2>

<ul class="item-list">
  <li>
    <div class="item-subsystem">Mar 2026</div>
    <div>
      <div><strong>fix missing run load for vcn0 in attr_data_get_block_locked()</strong></div>
      <div class="item-meta">
        When a compressed/sparse attribute has frame-aligned clusters, vcn0 can reside
        in a different segment than vcn. The code loaded vcn's segment but not vcn0's,
        causing run_lookup_entry() to return SPARSE_LCN and trigger WARN_ON(1).
        Signed-off: Konstantin Komarov.
      </div>
      <div class="item-links">
        <a href="https://syzkaller.appspot.com/bug?extid=c1e9aedbd913fadad617" target="_blank">syzbot</a>
      </div>
    </div>
  </li>
</ul>

<h2 id="atm">atm/lec</h2>

<ul class="item-list">
  <li>
    <div class="item-subsystem">Mar 2026</div>
    <div>
      <div><strong>fix use-after-free in sock_def_readable()</strong></div>
      <div class="item-meta">
        Race condition between lec_atm_close() clearing priv->lecd and concurrent
        dereference in send_to_lecd(). Fixed by converting priv->lecd to an
        RCU-protected pointer with rcu_assign_pointer() and rcu_dereference() guards.
        Signed-off: Andrew Morton.
      </div>
      <div class="item-links">
        <a href="https://lkml.kernel.org/r/20250909154903.522339-1-kartikey406@gmail.com" target="_blank">LKML</a>
        <a href="https://syzkaller.appspot.com/bug?extid=bbe6b99feefc3a0842de" target="_blank">syzbot</a>
      </div>
    </div>
  </li>
</ul>

<h2 id="hugetlb">hugetlbfs</h2>

<ul class="item-list">
  <li>
    <div class="item-subsystem">Sep 2025</div>
    <div>
      <div><strong>skip VMAs without shareable locks in hugetlb_vmdelete_list</strong></div>
      <div class="item-meta">
        hugetlb_vmdelete_list() proceeded with unmap_hugepage_range() even for VMAs
        without shareable locks, triggering assertion failures in huge_pmd_unshare().
        Fixed by properly skipping such VMAs. Suggested-by: Andrew Morton.
        Signed-off: Andrew Morton.
      </div>
      <div class="item-links">
        <a href="https://lkml.kernel.org/r/20250926033255.10930-1-kartikey406@gmail.com" target="_blank">LKML</a>
        <a href="https://syzkaller.appspot.com/bug?extid=f26d7c75c26ec19790e7" target="_blank">syzbot</a>
      </div>
    </div>
  </li>
</ul>

<h2 id="nsfs">nsfs</h2>

<ul class="item-list">
  <li>
    <div class="item-subsystem">Sep 2025</div>
    <div>
      <div><strong>handle inode number mismatches gracefully in file handles</strong></div>
      <div class="item-meta">
        Replaced VFS_WARN_ON_ONCE() with graceful error handling when file handles
        contain inode numbers that don't match the actual namespace inode.
        Suggested-by: Jan Kara. Reviewed-by: Jan Kara. Signed-off: Christian Brauner.
      </div>
      <div class="item-links">
        <a href="https://syzkaller.appspot.com/bug?extid=9eefe09bedd093f156c2" target="_blank">syzbot</a>
      </div>
    </div>
  </li>
</ul>

<h2 id="ocfs2">ocfs2</h2>

<ul class="item-list">
  <li>
    <div class="item-subsystem">Oct 2025</div>
    <div>
      <div><strong>fix out-of-bounds read in ocfs2_move_extents()</strong></div>
      <div class="item-meta">
        Fixed an out-of-bounds read in the ocfs2 extent move/defrag path.
        Reviewed-by: Mark Fasheh, Joseph Qi. Signed-off: Andrew Morton.
      </div>
      <div class="item-links">
        <a href="https://lkml.kernel.org/r/20251009154903.522339-1-kartikey406@gmail.com" target="_blank">LKML</a>
        <a href="https://syzkaller.appspot.com/bug?id=2959889e1f6e216585ce522f7e8bc002b46ad9e7" target="_blank">syzbot</a>
      </div>
    </div>
  </li>
</ul>

<h2 id="staging">staging</h2>

<ul class="item-list">
  <li>
    <div class="item-subsystem">May 2023</div>
    <div>
      <div><strong>staging: rts5208: remove newline in else/else-if</strong></div>
      <div class="item-meta">
        First kernel contribution — cleaned up checkpatch.pl warnings in the
        rts5208 staging driver. Reviewed-by: Dan Carpenter.
        Signed-off: Greg Kroah-Hartman.
      </div>
      <div class="item-links">
        <a href="https://lore.kernel.org/all/20230530135120.37637-1-kartikey406@gmail.com/" target="_blank">lore.kernel.org</a>
      </div>
    </div>
  </li>
</ul>
