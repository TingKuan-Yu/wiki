# from
- https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/28952/Image-Naming-conventions

# image download link
- https://dev.azure.com/E-OS/device/_packaging?_a=feed&feed=c1-11-main-images
- https://dev.azure.com/E-OS/device/_packaging?_a=feed&feed=c1-11-gen-images%40Local


---
For any **Release Target** (currently Tip of Tree (ToT) and **Release to Manufacturing (RTM))** we produce as set of Reference configurations:
- **Customer** - This build is configured for production signing, no debug and is what we would send to a customer
- **SFCL** (Software For Certification Labs) - This is a performance kernel with userdebug target/system used for cert labs such as AT&T, GCF/PTCRB, etc.
- **Developer** - This is a userdebug build that contains debug firmware and is what developers will generally use unless they need something more performant
- **Selfhost** - This is a user build with some debug tools, feedback app, etc. to enable frequent drops for the selfhost community prior to locking on final customer SKUS
- **MTEOS** (Manufacturing Test Engineering Operating System) - This is the OS used by the factory, configured and set up for factory test environment
- **NHLOS** (Non-High Level Operating System) - There is an entire set of FW that also follows this same methodology in referred to as NHLOS for simplicity

Not all of these will be enabled depending on what the team decides but they are all available. These will be enabled with rolling builds.

A Release Target then can have **Variants** that contain deltas from the Reference.  Examples are:
- **LKG** (Last Known Good) - This is just a fixed set of versions from the Release Target, useful for documentation and inclusion
- **3rdpty** - This is a variant specific to share with 3rd party Independent Software Vendors (ISVs) such as Spotify that are developing customizations for us but do not need to see competitive apps and/or have their own app installed causing debug problems
- **GEN** (generic or ‘open market’) - This is the variant that we deliver to customers if there are not Carrier requirements, appropriate for worldwide use
- **ATT** - This is a variant for ATT with their specific apps, configuration settings, feature removal and other changes they require

Additional concepts/terms:
- **Merge** – assuming from context we are talking a merge build; this is what pulls together system, target, firmware, and tools and creates a complete build. During this build signing is completed. This build generates the Combo and the OTA.
- **Combo** – one of the outputs of the merge build. This can be use to flash a device.
- **OTA** – another output of the merge build. This can be sideloaded onto a device but is normally published to GOTA for Over-the-Air installation onto devices.
- **OTA Differential** – not in Soren’s list, but I’m adding. Like the OTA above, but this is a diff between two builds. It is much smaller 1-250MB for the ones I’ve seen versus a couple GB for the full OTA so it will download over WiFi/cellular much faster. Overall install time is not affected that much as the “Optimizing Apps” portion of the update takes just as long. I think you can use this for sideloading, but I’m not certain.
- **Debug** – various components can be user or userdebug (I think there is also a really slow third option for deep debugging…sort of like a Windows Checked Build). Like in most software, the debug versions are slower; to this end, the different configurations (Customer, SFCL, etc.) have different components that we use debug versions for.