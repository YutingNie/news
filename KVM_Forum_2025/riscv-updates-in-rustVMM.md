# KVM Forum 2025 | RISC-V updates in rust-vmm Community

From September 3 to 4, 2025, the KVM Forum, one of the most influential events
in the field of virtualization, was successfully held in Milan, Italy. The
conference featured updates on the latest developments in the KVM
virtualization software stack, future roadmap planning, and other key topics.
Birds of a Feather (BoF) sessions were also organized to facilitate in-depth
discussions on critical directions and strategic decisions. As a major
gathering for the KVM community, the KVM Forum promotes efficient communication
and collaboration among kernel, platform, and application practitioners.

On September 3 at 2:00 PM local time, Ruoqing He, leader of the OERV
virtualization team at the Institute of Software, Chinese Academy of Sciences
(ISCAS) and a maintainer of RustVMM, delivered a presentation titled "rust-vmm:
updates, adoption, and future directions" alongside Stefano Garzarella from Red
Hat and Patrick Roy from AWS in Aula Osvaldo 3.0.2 at Politecnico di Milano.
Ruoqing He focused on two key initiatives within the rust-vmm community: the
evolution of the RISC-V architecture and the monorepo initiative. He provided
an overview of the current state of RISC-V virtualization technology, discussed
existing challenges, and highlighted the achievements made by his team in
advancing the development of the related software stack.

<img title="" src=".\Images\image1.png" alt="">  

## What is rust-vmm

An open-source project that empowers the community to build custom Virtual
Machine Monitors (VMMs) and hypervisors by providing a set of virtualization
components that any project can use to quickly develop virtualization
solutions. It significantly reduces the cost and risk of building
virtualization solutions from scratch. The project offers clean, secure
abstractions and supporting infrastructure around mainstream virtualization
kernel interfaces(including KVM, Microsoft Hyper-V, and Xen) making it suitable
for prototyping, product development, and reusing virtualization capabilities
across multiple platforms.

## Why choose rust-vmm

- Reduce code duplication: It avoids redundant development efforts across
  different projects by componentizing common virtualization capabilities.

- Faster development: Ready-to-use foundational libraries and unified
  interfaces significantly speed up the process from prototyping to production.

- Clean interface:  Well-designed APIs make integration straightforward and
  long-term maintenance more manageable.

## Components of rust-vmm

**Core Virtualization Components:**

- **KVM Wrappers**: `kvm-ioctls` and `kvm-bindings` (provide safe,
  Rust-friendly access to Linux KVM kernel interfaces for higher-level
applications)

- **Microsoft Hyper-V Wrappers**: `mshv-ioctls` and `mshv-bindings` (offer
  bindings and encapsulated interfaces for Microsoft Hyper-V)

- **Xen Wrappers**: `xen`, `xen-ioctls`, `xen-bindings`, etc. (deliver
  Rust-based implementations for Xen hypercalls and related interfaces)

- **Linux Kernel Loader**: `linux-loader` (handles booting and loading of guest
  kernels or initial images into memory)

**Resource Management:**

- **VM Resource Allocator**: `vm-allocator` ( manages the allocation of
  resources such as MMIO/PIO addresses and device/interrupt IDs)

- **Memory Management**: `vm-memory` ( abstracts and manages guest physical
  memory, including memory mapping and access operations)

**Use Cases:**

- Building lightweight or customized VMMs/hypervisors from the ground up.

- Reusing high-level logic across multiple hypervisor backends (KVM, MSHV,
  Xen).

- Rapid prototyping, experimenting with new features, or embedding
  virtualization capabilities into products and platforms.

## Adoption of rust-vmm

The adoption of rust-vmm now spans the entire stack: from production-grade
Virtual Machine Monitors (VMMs) to container sandboxes, device backends, image
tools, and development utilities:

- **Firecracker** uses rust-vmm components to deploy workloads in lightweight
  microVMs, offering stronger isolation and faster startup

- **Cloud Hypervisor**, an open-source VMM implemented in Rust and built on
  rust-vmm crates, supports both KVM and Microsoft Hypervisor (MSHV).

- **libkrun** is a dynamic library that allows applications to run processes in
  a partially isolated environment using KVM on Linux and HVF on macOS/ARM64.

- **Kata Containers’ Dragonball Sandbox** is a lightweight VMM based on KVM,
  optimized specifically for container workloads.

On the device and filesystem side, the **vhost-user ecosystem**(including
projects such as `rust-vmm/vhost-device` and `virtiofsd`)can interoperate with
VMMs that implement vhost-user frontends, such as QEMU and Cloud Hypervisor.

Within the image and storage toolchain:

- **hreitz/imago** provides access to VM image formats including raw and qcow2.

- **dragonflyoss/nydus** offers fast and secure container image services via
  FUSE or virtiofs for runc and Kata Containers environments.

Additionally, developer tools like **archlinux/vmexec**—a zero-setup CLI
utility that executes single commands in disposable virtual machines—further
demonstrate the versatility of rust-vmm. These implementations highlight
rust-vmm’s broad value in enabling cross-backend portability, enhancing
security and testability, and improving engineering efficiency.

---

## monorepo

<img title="" src=".\Images\image2.png" alt="">  

The rust-vmm community maintains over 20 core repositories. Over the past year,
the OERV team has consolidated half of these into several functionally
organized monorepos, steadily progressing toward a unified rust-vmm monorepo
structure.

<img title="" src=".\Images\image3.png" alt=""> 

## Progress on RISC-V Support

Since April 2024, the OERV team has contributed over 100,000 lines of code to
enable RISC-V architecture support within the rust-vmm ecosystem. Covering
areas from infrastructure (rust-vmm-ci, rust-vmm-container) to core components
(such as kvm-bindings, kvm-ioctls, and linux-loader), these efforts over seven
months have established RISC-V as the third officially supported
architecture—after x86 and ARM—within the KVM virtualization framework.

<img title="" src=".\Images\image4.png" alt="">  

Looking ahead, the OERV team will continue to contribute to and maintain the
RISC-V support within the rust-vmm community, extending its coverage to other
key modules such as vhost, virtio, and vfio. In parallel, the team will help
evolve the RISC-V infrastructure by transitioning from the current x86-based
emulated CI environment to real RISC-V hardware.
<img title="" src=".\Images\image5.png" alt="">  

rust-vmm：

https://github.com/rust-vmm/community

slides：

https://gitlab.com/qemu-project/kvm-forum/-/raw/main/_attachments/2025/KVM_Forum_2_G52TiSW.pdf

full speech video: 

https://www.youtube.com/watch?v=IYfR1jYeM1g
