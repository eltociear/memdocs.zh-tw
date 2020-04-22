---
title: '[資源總管] 預設清查類別'
titleSuffix: Configuration Manager
description: 顯示出現在 [資源總管] 中的類別
ms.date: 11/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d333f4c-0f85-4278-b421-064cf01529a5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 81cf8e1779e072d3eee6a5ed7080b6a63fd07451
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690176"
---
# <a name="resource-explorer-default-inventory-classes"></a>[資源總管] 預設清查類別

適用於：  Configuration Manager (最新分支)

本文描述 [資源總管] 中的預設清查類別。

以下為預設的清查類別：

## <a name="1394-controller"></a>1394 控制器

命名空間：root\cimv2

類別 Win32_1394Controller


- (字串) DeviceID

- (UInt16) Availability

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (字串) Manufacturer

- (UInt32) MaxNumberControlled

- (字串) Name

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (日期時間) TimeOfLastReset



## <a name="account-sid"></a>帳戶 SID

命名空間：root\cimv2

類別 Win32_AccountSID

- (字串) Element

- (字串) Setting



## <a name="activesync-service"></a>ActiveSync 服務

命名空間：root\SmsDm

類別 SMS_ActiveSyncService


- (UInt32) MajorVersion

- (UInt32) MinorVersion

- (字串) LastSyncTime



## <a name="amt-agent"></a>AMT 代理程式

命名空間：root\cimv2\sms

類別 SMS_AMTObject


- (UInt32) DeviceID

- (字串) AMT

- (字串) AMTApps

- (字串) BiosVersion

- (字串) BuildNumber

- (字串) Flash

- (字串) LegacyMode

- (字串) Netstack

- (UInt32) ProvisionMode

- (UInt32) ProvisionState

- (字串) RecoveryBuildNum

- (字串) RecoveryVersion

- (字串) Sku

- (UInt32) TLSMode

- (字串) VendorID

- (UInt32) ZTCEnabled



## <a name="appv-client-application"></a>AppV 用戶端應用程式

命名空間：root\AppV

類別 AppvClientApplication


- (字串) ApplicationId

- (字串) PackageId

- (字串) PackageVersionId

- (布林值) EnabledForUser

- (布林值) EnabledGlobally

- (字串) Name

- (字串) TargetPath

- (字串) Version



## <a name="appv-client-package"></a>AppV 用戶端套件

命名空間：root\AppV

類別 AppvClientPackage


- (字串) PackageId

- (字串) VersionId

- (字串) Assets[]

- (字串) DeploymentMachineData

- (字串) DeploymentUserData

- (布林值) HasAssetIntelligence

- (布林值) InUse

- (布林值) IsPublishedGlobally

- (布林值) IsPublishedToUser

- (字串) Name

- (UInt64) PackageSize

- (字串) Path

- (UInt16) PercentLoaded

- (字串) UserConfigurationData

- (字串) Version



## <a name="autostart-software"></a>自動啟動軟體

命名空間：root\cimv2\sms

類別 SMS_AutoStartSoftware


- (字串) FilePropertiesHash

- (字串) BinFileVersion

- (字串) BinProductVersion

- (字串) Description

- (字串) FileName

- (字串) FilePropertiesHashEx

- (字串) FileVersion

- (字串) Location

- (字串) Product

- (字串) ProductVersion

- (字串) Publisher

- (字串) StartupType

- (字串) StartupValue



## <a name="baseboard"></a>基板

命名空間：root\cimv2

類別 Win32_BaseBoard


- (字串) Tag

- (字串) Caption

- (字串) ConfigOptions[]

- (字串) Description

- (布林值) HostingBoard

- (布林值) HotSwappable

- (日期時間) InstallDate

- (字串) Manufacturer

- (字串) Model

- (字串) Name

- (字串) OtherIdentifyingInfo

- (字串) PartNumber

- (布林值) PoweredOn

- (字串) Product

- (布林值) Removable

- (布林值) Replaceable

- (字串) RequirementsDescription

- (布林值) RequiresDaughterBoard

- (字串) SerialNumber

- (字串) SKU

- (字串) SlotLayout

- (布林值) SpecialRequirements

- (字串) Status

- (字串) Version



## <a name="battery"></a>電池

命名空間：root\cimv2

類別 Win32_Battery


- (字串) DeviceID

- (UInt16) Availability

- (UInt16) BatteryStatus

- (字串) Caption

- (UInt16) Chemistry

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (UInt32) DesignCapacity

- (UInt64) DesignVoltage

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (UInt16) EstimatedChargeRemaining

- (UInt32) EstimatedRunTime

- (UInt32) ExpectedLife

- (UInt32) FullChargeCapacity

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (UInt32) MaxRechargeTime

- (字串) Name

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (字串) SmartBatteryVersion

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (UInt32) TimeOnBattery

- (UInt32) TimeToFullCharge



## <a name="bitlocker"></a>BitLocker

命名空間：root\cimv2\security\MicrosoftVolumeEncryption

類別 Win32_EncryptableVolume


- (字串) DeviceID

- (字串) DriveLetter

- (字串) PersistentVolumeID

- (UInt32) ProtectionStatus



## <a name="bitlocker-encryption-details"></a>BitLocker 加密詳細資料

命名空間：root\cimv2

類別 Win32_BitLockerEncryptionDetails


- (字串) BitlockerPersistentVolumeId

- (SInt32) Compliant

- (SInt32) ConversionStatus

- (字串) DeviceId

- (字串) DriveLetter

- (SInt32) EncryptionMethod

- (字串) EnforcePolicyDate

- (布林值) IsAutoUnlockEnabled

- (SInt32) KeyProtectorTypes[]

- (字串) MbamPersistentVolumeId

- (SInt32) MbamVolumeType

- (字串) NoncomplianceDetectedDate

- (SInt32) ProtectionStatus

- (SInt32) ReasonsForNonCompliance[]



## <a name="bitlocker-policy"></a>BitLocker 原則

命名空間：root\cimv2

類別 Win32Reg_MBAMPolicy


- (字串) EncodedComputerName

- (UInt32) EncryptionMethod

- (UInt32) FixedDataDriveAutoUnlock

- (UInt32) FixedDataDriveEncryption

- (UInt32) FixedDataDrivePassphrase

- (字串) KeyName

- (字串) LastConsoleUser

- (UInt32) MBAMMachineError

- (UInt32) MBAMPolicyEnforced

- (UInt32) OsDriveEncryption

- (UInt32) OsDriveProtector

- (日期時間) UserExemptionDate



## <a name="boot-configuration"></a>開機設定

命名空間：root\cimv2

類別 Win32_BootConfiguration


- (字串) Name

- (字串) BootDirectory

- (字串) ConfigurationPath

- (字串) Description

- (字串) LastDrive

- (字串) ScratchDirectory

- (字串) SettingID

- (字串) TempDirectory



## <a name="browser-helper-object"></a>瀏覽器協助程式物件

命名空間：root\cimv2\sms

類別 SMS_BrowserHelperObject


- (字串) FilePropertiesHash

- (字串) BinFileVersion

- (字串) BinProductVersion

- (字串) CLSID

- (字串) Description

- (字串) FileName

- (字串) FilePropertiesHashEx

- (字串) FileVersion

- (字串) Product

- (字串) ProductVersion

- (字串) Publisher

- (字串) Version



## <a name="ccm_rax"></a>CCM_RAX

命名空間：root\ccm\cimodels

類別 CCM_RAXInfo


- (字串) AppID

- (字串) FeedURL

- (字串) UserSID



## <a name="cd-rom"></a>CD-ROM

命名空間：root\cimv2

類別 Win32_CDROMDrive


- (字串) DeviceID

- (UInt16) Availability

- (UInt16) Capabilities[]

- (字串) CapabilityDescriptions[]

- (字串) Caption

- (字串) CompressionMethod

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (UInt64) DefaultBlockSize

- (字串) Description

- (字串) Drive

- (布林值) DriveIntegrity

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (字串) ErrorMethodology

- (UInt16) FileSystemFlags

- (UInt32) FileSystemFlagsEx

- (字串) ID

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (字串) Manufacturer

- (UInt64) MaxBlockSize

- (UInt32) MaximumComponentLength

- (UInt64) MaxMediaSize

- (布林值) MediaLoaded

- (字串) MediaType

- (UInt64) MinBlockSize

- (字串) Name

- (布林值) NeedsCleaning

- (UInt32) NumberOfMediaSupported

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (字串) RevisionLevel

- (UInt32) SCSIBus

- (UInt16) SCSILogicalUnit

- (UInt16) SCSIPort

- (UInt16) SCSITargetId

- (UInt64) Size

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (字串) VolumeName

- (字串) VolumeSerialNumber



## <a name="client-events"></a>用戶端事件

命名空間：root\ccm\invagt

類別 ClientEvents


- (字串) EventName

- (UInt16) Count



## <a name="computer-system"></a>電腦系統

命名空間：root\cimv2

類別 Win32_ComputerSystem


- (字串) Name

- (UInt16) AdminPasswordStatus

- (布林值) AutomaticResetBootOption

- (布林值) AutomaticResetCapability

- (UInt16) BootOptionOnLimit

- (UInt16) BootOptionOnWatchDog

- (布林值) BootROMSupported

- (字串) BootupState

- (字串) Caption

- (UInt16) ChassisBootupState

- (SInt16) CurrentTimeZone

- (布林值) DaylightInEffect

- (字串) Description

- (字串) Domain

- (UInt16) DomainRole

- (UInt16) FrontPanelResetStatus

- (布林值) InfraredSupported

- (字串) InitialLoadInfo[]

- (日期時間) InstallDate

- (UInt16) KeyboardPasswordStatus

- (字串) LastLoadInfo

- (字串) Manufacturer

- (字串) Model

- (字串) NameFormat

- (布林值) NetworkServerModeEnabled

- (UInt32) NumberOfProcessors

- (字串) OEMLogoBitmap

- (字串) OEMStringArray[]

- (SInt64) PauseAfterReset

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt16) PowerOnPasswordStatus

- (UInt16) PowerState

- (UInt16) PowerSupplyState

- (字串) PrimaryOwnerContact

- (字串) PrimaryOwnerName

- (UInt16) ResetCapability

- (SInt16) ResetCount

- (SInt16) ResetLimit

- (字串) Roles[]

- (字串) Status

- (字串) SupportContactDescription[]

- (UInt16) SystemStartupDelay

- (字串) SystemStartupOptions[]

- (UInt8) SystemStartupSetting

- (字串) SystemType

- (UInt16) ThermalState

- (UInt64) TotalPhysicalMemory

- (字串) UserName

- (UInt16) WakeUpType



## <a name="computer-system-ex"></a>電腦系統 Ex

命名空間：root\cimv2

類別 CCM_ComputerSystemExtended


- (字串) Name

- (UInt16) PCSystemType



## <a name="computer-system-product"></a>電腦系統產品

命名空間：root\cimv2

類別 Win32_ComputerSystemProduct


- (字串) IdentifyingNumber

- (字串) Name

- (字串) Version

- (字串) Caption

- (字串) Description

- (字串) SKUNumber

- (字串) UUID

- (字串) Vendor



## <a name="sms-advanced-client-ports"></a>SMS 進階用戶端連接埠

命名空間：root\cimv2

類別 Win32Reg_SMSAdvancedClientPorts


- (字串) InstanceKey

- (UInt32) HttpsPortName

- (UInt32) PortName



## <a name="sms-advanced-client-ssl-configurations"></a>SMS 進階用戶端 SSL 設定

命名空間：root\cimv2

類別 Win32Reg_SMSAdvancedClientSSLConfiguration


- (字串) InstanceKey

- (字串) CertificateSelectionCriteria

- (字串) CertificateStore

- (UInt32) ClientAlwaysOnInternet

- (UInt32) HttpsStateFlags

- (字串) InternetMPHostName

- (UInt32) SelectFirstCertificate



## <a name="sms-advanced-client-state"></a>SMS 進階用戶端狀態

命名空間：root\ccm

類別 CCM_InstalledComponent


- (字串) Name

- (字串) DisplayName

- (字串) Version



## <a name="connected-device"></a>連線的裝置

命名空間：root\SmsDm

類別 SMS_ActiveSyncConnectedDevice


- (字串) DeviceOEMInfo

- (字串) DeviceType

- (字串) OS_Major

- (字串) OS_Minor

- (字串) OS_Platform

- (字串) ProcessorArchitecture

- (字串) ProcessorLevel

- (字串) ProcessorRevision

- (字串) InstalledClientID

- (字串) InstalledClientServer

- (字串) InstalledClientVersion

- (字串) LastSyncTime

- (字串) OS_AdditionalInfo

- (字串) OS_Build



## <a name="sms_defaultbrowser"></a>SMS_DefaultBrowser

命名空間：root\cimv2\sms

類別 SMS_DefaultBrowser


- (字串) BrowserProgId



## <a name="desktop"></a>桌面

命名空間：root\cimv2

類別 Win32_Desktop


- (字串) Name

- (UInt32) BorderWidth

- (字串) Caption

- (布林值) CoolSwitch

- (UInt32) CursorBlinkRate

- (字串) Description

- (布林值) DragFullWindows

- (UInt32) GridGranularity

- (UInt32) IconSpacing

- (字串) IconTitleFaceName

- (UInt32) IconTitleSize

- (布林值) IconTitleWrap

- (字串) Pattern

- (布林值) ScreenSaverActive

- (字串) ScreenSaverExecutable

- (布林值) ScreenSaverSecure

- (UInt32) ScreenSaverTimeout

- (字串) SettingID

- (字串) Wallpaper

- (布林值) WallpaperStretched

- (布林值) WallpaperTiled



## <a name="desktop-monitor"></a>桌上型監視器

命名空間：root\cimv2

類別 Win32_DesktopMonitor


- (字串) DeviceID

- (UInt16) Availability

- (UInt32) Bandwidth

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (UInt16) DisplayType

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (日期時間) InstallDate

- (布林值) IsLocked

- (UInt32) LastErrorCode

- (字串) MonitorManufacturer

- (字串) MonitorType

- (字串) Name

- (UInt32) PixelsPerXLogicalInch

- (UInt32) PixelsPerYLogicalInch

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt32) ScreenHeight

- (UInt32) ScreenWidth

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName



## <a name="device-info"></a>裝置資訊

命名空間：保留

類別 Device_Info


- (字串) CertExpiry

- (字串) DeviceName

- (字串) Manufacturer

- (字串) Model

- (字串) OS



## <a name="mdm-devdetail"></a>MDM DevDetail

命名空間：root\cimv2\mdm\dmmap

類別 MDM_DevDetail_Ext01


- (字串) InstanceID

- (字串) ParentID

- (字串) DeviceHardwareData

- (字串) WLANMACAddress



## <a name="disk"></a>磁碟

命名空間：root\cimv2

類別 Win32_DiskDrive


- (字串) DeviceID

- (UInt16) Availability

- (UInt32) BytesPerSector

- (UInt16) Capabilities[]

- (字串) CapabilityDescriptions[]

- (字串) Caption

- (字串) CompressionMethod

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (UInt64) DefaultBlockSize

- (字串) Description

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (字串) ErrorMethodology

- (UInt32) Index

- (日期時間) InstallDate

- (字串) InterfaceType

- (UInt32) LastErrorCode

- (字串) Manufacturer

- (UInt64) MaxBlockSize

- (UInt64) MaxMediaSize

- (布林值) MediaLoaded

- (字串) MediaType

- (UInt64) MinBlockSize

- (字串) Model

- (字串) Name

- (布林值) NeedsCleaning

- (UInt32) NumberOfMediaSupported

- (UInt32) Partitions

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt32) SCSIBus

- (UInt16) SCSILogicalUnit

- (UInt16) SCSIPort

- (UInt16) SCSITargetId

- (UInt32) SectorsPerTrack

- (UInt64) Size

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (UInt64) TotalCylinders

- (UInt32) TotalHeads

- (UInt64) TotalSectors

- (UInt64) TotalTracks

- (UInt32) TracksPerCylinder



## <a name="partition"></a>分割區

命名空間：root\cimv2

類別 Win32_DiskPartition


- (字串) DeviceID

- (UInt16) Access

- (UInt16) Availability

- (UInt64) BlockSize

- (布林值) Bootable

- (布林值) BootPartition

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (UInt32) DiskIndex

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (字串) ErrorMethodology

- (UInt32) HiddenSectors

- (UInt32) Index

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (字串) Name

- (UInt64) NumberOfBlocks

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (布林值) PrimaryPartition

- (字串) Purpose

- (布林值) RewritePartition

- (UInt64) Size

- (UInt64) StartingOffset

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (字串) Type



## <a name="dma"></a>DMA

命名空間：root\cimv2

類別 Win32_DeviceMemoryAddress

- (UInt64) StartingAddress

- (字串) Caption

- (字串) Description

- (UInt64) EndingAddress

- (日期時間) InstallDate

- (字串) MemoryType

- (字串) Name

- (字串) Status



## <a name="dma-channel"></a>DMA 通道

命名空間：root\cimv2

類別 Win32_DMAChannel


- (UInt32) DMAChannel

- (UInt16) AddressSize

- (UInt16) Availability

- (布林值) BurstMode

- (UInt16) ByteMode

- (字串) Caption

- (UInt16) ChannelTiming

- (字串) Description

- (日期時間) InstallDate

- (UInt32) MaxTransferSize

- (字串) Name

- (UInt32) Port

- (字串) Status

- (UInt16) TransferWidths[]

- (UInt16) TypeCTiming

- (UInt16) WordMode



## <a name="driver---vxd"></a>驅動程式 - VxD

命名空間：root\cimv2

類別 Win32_DriverVXD


- (字串) Name

- (字串) SoftwareElementID

- (UInt16) SoftwareElementState

- (UInt16) TargetOperatingSystem

- (字串) Version

- (字串) BuildNumber

- (字串) Caption

- (字串) CodeSet

- (字串) Control

- (字串) Description

- (字串) DeviceDescriptorBlock

- (字串) IdentificationCode

- (日期時間) InstallDate

- (字串) LanguageEdition

- (字串) Manufacturer

- (字串) OtherTargetOS

- (字串) PM_API

- (字串) SerialNumber

- (UInt32) ServiceTableSize

- (字串) Status

- (字串) V86_API



## <a name="embedded-device-information"></a>內嵌的裝置資訊

命名空間：root\cimv2\sms

類別 CCM_EmbeddedDeviceInformation


- (字串) DeviceType

- (字串) Model

- (字串) OEMName



## <a name="environment"></a>環境

命名空間：root\cimv2

類別 Win32_Environment


- (字串) Name

- (字串) UserName

- (字串) Caption

- (字串) Description

- (日期時間) InstallDate

- (字串) Status

- (布林值) SystemVariable

- (字串) VariableValue



## <a name="firmware"></a>韌體

命名空間：root\cimv2\sms

類別 SMS_Firmware


- (布林值) UEFI

- (布林值) SecureBoot



## <a name="usm-folder-redirection-health"></a>USM 資料夾重新導向健全狀況

命名空間：root\cimv2\sms

類別 SMS_FolderRedirectionHealth


- (字串) FolderName

- (字串) SID

- (UInt8) HealthStatus

- (日期時間) LastSuccessfulSyncTime

- (UInt8) LastSyncStatus

- (日期時間) LastSyncTime

- (布林值) OfflineAccessEnabled

- (字串) OfflineFileNameFolderGUID

- (布林值) Redirected



## <a name="ide-controller"></a>IDE 控制器

命名空間：root\cimv2

類別 Win32_IDEController


- (字串) DeviceID

- (UInt16) Availability

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (字串) Manufacturer

- (UInt32) MaxNumberControlled

- (字串) Name

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (日期時間) TimeOfLastReset



## <a name="add-remove-programs-64"></a>新增/移除程式 (64)

命名空間：root\cimv2

類別 Win32Reg_AddRemovePrograms64


- (字串) ProdID

- (字串) DisplayName

- (字串) InstallDate

- (字串) Publisher

- (字串) Version



## <a name="add-remove-programs"></a>新增/移除程式

命名空間：root\cimv2

類別 Win32Reg_AddRemovePrograms


- (字串) ProdID

- (字串) DisplayName

- (字串) InstallDate

- (字串) Publisher

- (字串) Version



## <a name="installed-executable"></a>已安裝的可執行檔

命名空間：root\cimv2\sms

類別 SMS_InstalledExecutable


- (字串) ExecutableName

- (字串) ProductCode

- (字串) BinFileVersion

- (字串) BinProductVersion

- (字串) Description

- (字串) FilePropertiesHash

- (字串) FilePropertiesHashEx

- (UInt32) FileSize

- (字串) FileVersion

- (布林值) HasPatchAdded

- (字串) InstalledFilePath

- (布林值) IsSystemFile

- (布林值) IsVitalFile

- (UInt32) Language

- (字串) Product

- (字串) ProductVersion

- (字串) Publisher



## <a name="installed-software"></a>已安裝的軟體

命名空間：root\cimv2\sms

類別 SMS_InstalledSoftware


- (字串) SoftwareCode

- (字串) ARPDisplayName

- (字串) ChannelCode

- (字串) ChannelID

- (字串) CM_DSLID

- (字串) EvidenceSource

- (日期時間) InstallDate

- (UInt32) InstallDirectoryValidation

- (字串) InstalledLocation

- (字串) InstallSource

- (UInt32) InstallType

- (UInt32) Language

- (字串) LocalPackage

- (字串) MPC

- (UInt32) OsComponent

- (字串) PackageCode

- (字串) ProductID

- (字串) ProductName

- (字串) ProductVersion

- (字串) Publisher

- (字串) RegisteredUser

- (字串) ServicePack

- (字串) SoftwarePropertiesHash

- (字串) SoftwarePropertiesHashEx

- (字串) UninstallString

- (字串) UpgradeCode

- (UInt32) VersionMajor

- (UInt32) VersionMinor



## <a name="irq-table"></a>IRQ 表

命名空間：root\cimv2

類別 Win32_IRQResource


- (UInt32) IRQNumber

- (UInt16) Availability

- (字串) Caption

- (字串) Description

- (布林值) Hardware

- (日期時間) InstallDate

- (字串) Name

- (布林值) Shareable

- (字串) Status

- (UInt16) TriggerLevel

- (UInt16) TriggerType

- (UInt32) Vector



## <a name="keyboard"></a>鍵盤

命名空間：root\cimv2

類別 Win32_Keyboard


- (字串) DeviceID

- (UInt16) Availability

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (日期時間) InstallDate

- (布林值) IsLocked

- (UInt32) LastErrorCode

- (字串) Layout

- (字串) Name

- (UInt16) NumberOfFunctionKeys

- (UInt16) Password

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName



## <a name="load-order-group"></a>載入順序群組

命名空間：root\cimv2

類別 Win32_LoadOrderGroup


- (字串) Name

- (字串) Caption

- (字串) Description

- (布林值) DriverEnabled

- (UInt32) GroupOrder

- (日期時間) InstallDate

- (字串) Status



## <a name="logical-disk"></a>邏輯磁碟

命名空間：root\cimv2\sms

類別 SMS_LogicalDisk


- (字串) DeviceID

- (UInt16) Access

- (UInt16) Availability

- (UInt64) BlockSize

- (字串) Caption

- (布林值) Compressed

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (UInt32) DriveType

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (字串) ErrorMethodology

- (字串) FileSystem

- (UInt64) FreeSpace

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (UInt32) MaximumComponentLength

- (UInt32) MediaType

- (字串) Name

- (UInt64) NumberOfBlocks

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (字串) ProviderName

- (字串) Purpose

- (UInt64) Size

- (字串) Status

- (UInt16) StatusInfo

- (布林值) SupportsFileBasedCompression

- (字串) SystemName

- (字串) VolumeName

- (字串) VolumeSerialNumber



## <a name="memory"></a>記憶體

命名空間：root\cimv2

類別 CCM_LogicalMemoryConfiguration


- (字串) Name

- (UInt64) AvailableVirtualMemory

- (UInt64) TotalPageFileSpace

- (UInt64) TotalPhysicalMemory

- (UInt64) TotalVirtualMemory



## <a name="device-bluetooth"></a>裝置 Bluetooth

命名空間：保留

類別 Device_Bluetooth


- (布林值) Enabled



## <a name="device-camera"></a>裝置相機

命名空間：保留

類別 Device_Camera


- (布林值) Enabled



## <a name="device-certificates"></a>裝置憑證

命名空間：保留

類別 Device_Certificates


- (字串) Thumbprint

- (字串) Type

- (字串) IssuedBy

- (字串) IssuedTo

- (日期時間) ValidFrom

- (日期時間) ValidTo



## <a name="device-client"></a>裝置用戶端

命名空間：保留

類別 Device_Client


- (布林值) DownloadWhenRoaming

- (布林值) SyncWhenRoaming



## <a name="device-client-agent-version"></a>裝置用戶端代理程式版本

命名空間：保留

類別 Device_ClientAgentVersion


- (字串) Version



## <a name="device-computer-system"></a>裝置電腦系統

命名空間：保留

類別 Device_ComputerSystem


- (字串) CellularTechnology

- (字串) DeviceClientID

- (字串) DeviceManufacturer

- (字串) DeviceModel

- (字串) DMVersion

- (字串) FirmwareVersion

- (字串) HardwareVersion

- (字串) IMEI

- (字串) IMSI

- (UInt8) IsActivationLockEnabled

- (UInt8) Jailbroken

- (字串) MEID

- (字串) OEM

- (字串) PhoneNumber

- (字串) PlatformType

- (UInt32) ProcessorArchitecture

- (UInt32) ProcessorLevel

- (UInt32) ProcessorRevision

- (字串) Product

- (字串) ProductVersion

- (字串) SerialNumber

- (字串) SoftwareVersion

- (字串) SubscriberCarrierNetwork



## <a name="device-display"></a>裝置顯示

命名空間：保留

類別 Device_Display


- (UInt32) HorizontalResolution

- (UInt64) NumberOfColors

- (UInt32) VerticalResolution



## <a name="device-email"></a>裝置電子郵件

命名空間：保留

類別 Device_Email


- (字串) OwnerEmailAddress

- (字串) SyncDomain

- (字串) SyncServer

- (字串) SyncUser

- (字串) Type



## <a name="device-encryption"></a>裝置加密

命名空間：保留

類別 Device_Encryption


- (UInt32) EmailEncryptionAlgorithm

- (UInt32) EmailEncryptionNegotiation

- (布林值) EmailEncryptionRequired

- (布林值) EmailSigningAlgorithm

- (布林值) EmailSigningRequired

- (布林值) EncryptionCompliance

- (布林值) PhoneMemoryEncrypted

- (布林值) StorageCardEncrypted



## <a name="device-exchange"></a>裝置交換

命名空間：保留

類別 Device_Exchange


- (布林值) ConflictResolution

- (SInt32) HTMLEmailTruncation

- (UInt32) MailFormat

- (UInt32) MaxCalendarAge

- (UInt32) MaxEmailAge

- (SInt32) MaxMailFileAttachmentSize

- (UInt32) OffPeakSyncFrequency

- (UInt32) PeakDays

- (字串) PeakEndTime

- (字串) PeakStartTime

- (UInt32) PeakSyncFrequency

- (SInt32) PlainTextEmailTruncation

- (布林值) SendEmailImmediately

- (布林值) SyncCalendar

- (布林值) SyncContacts

- (布林值) SyncEmail

- (布林值) SyncTasks

- (布林值) SyncWhenRoaming



## <a name="device-installed-applications"></a>裝置安裝的應用程式

命名空間：保留

類別 Device_InstalledApplications


- (字串) Name

- (字串) Version



## <a name="device-irda"></a>裝置 IrDA

命名空間：保留

類別 Device_IrDA


- (布林值) Enabled



## <a name="mobile-device-location"></a>行動裝置位置

命名空間：保留

類別 MDM_RemoteFind


- (Real32) Latitude

- (Real32) Longitude



## <a name="device-memory"></a>裝置記憶體

命名空間：保留

類別 Device_Memory


- (UInt64) ProgramFree

- (UInt64) ProgramTotal

- (UInt64) RemovableStorageFree

- (UInt64) RemovableStorageTotal

- (UInt64) StorageFree

- (UInt64) StorageTotal



## <a name="device-os-information"></a>裝置作業系統資訊

命名空間：保留

類別 Device_OSInformation


- (字串) Language

- (字串) Platform

- (字串) Version



## <a name="device-password"></a>裝置密碼

命名空間：保留

類別 Device_Password


- (布林值) AllowRecoveryPassword

- (UInt32) AutolockTimeout

- (布林值) Enabled

- (UInt32) Expiration

- (UInt32) History

- (UInt32) MaxAttemptsBeforeWipe

- (UInt32) MinComplexChars

- (UInt32) MinLength

- (UInt8) PasswordQuality

- (UInt32) Type



## <a name="device-policy"></a>裝置原則

命名空間：保留

類別 Device_Policy


- (字串) Name

- (布林值) Enforced



## <a name="device-power"></a>裝置電源

命名空間：保留

類別 Device_Power


- (UInt32) BacklightACTimeout

- (UInt32) BacklightBatTimeout

- (SInt32) BackupPercent

- (SInt32) BatteryPercent



## <a name="mobile-device-security-status"></a>行動裝置安全性狀態

命名空間：保留

類別 MDM_SecurityStatus


- (UInt32) HardwareEncryptionCaps

- (UInt8) PasscodeCompliant

- (UInt8) PasscodeCompliantWithProfiles

- (UInt8) PasscodePresent

- (UInt8) RequireEncryption



## <a name="device-windows-security-policy"></a>裝置 Windows 安全性原則

命名空間：保留

類別 Device_WindowsSecurityPolicy


- (UInt32) ID

- (字串) Name

- (UInt32) Value



## <a name="device-wlan"></a>裝置 WLAN

命名空間：保留

類別 Device_WLAN


- (布林值) Enabled

- (字串) EthernetMAC

- (字串) WiFiMAC



## <a name="modem"></a>數據機

命名空間：root\cimv2

類別 Win32_POTSModem


- (字串) DeviceID

- (UInt16) AnswerMode

- (字串) AttachedTo

- (UInt16) Availability

- (字串) BlindOff

- (字串) BlindOn

- (字串) Caption

- (字串) CompatibilityFlags

- (UInt16) CompressionInfo

- (字串) CompressionOff

- (字串) CompressionOn

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) ConfigurationDialog

- (字串) CountriesSupported[]

- (字串) CountrySelected

- (字串) CurrentPasswords[]

- (字串) DCB

- (字串) Default

- (字串) Description

- (字串) DeviceLoader

- (字串) DeviceType

- (UInt16) DialType

- (日期時間) DriverDate

- (布林值) ErrorCleared

- (字串) ErrorControlForced

- (UInt16) ErrorControlInfo

- (字串) ErrorControlOff

- (字串) ErrorControlOn

- (字串) ErrorDescription

- (字串) FlowControlHard

- (字串) FlowControlOff

- (字串) FlowControlSoft

- (字串) InactivityScale

- (UInt32) InactivityTimeout

- (UInt32) Index

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (UInt32) MaxBaudRateToPhone

- (UInt32) MaxBaudRateToSerialPort

- (UInt16) MaxNumberOfPasswords

- (字串) Model

- (字串) ModemInfPath

- (字串) ModemInfSection

- (字串) ModulationBell

- (字串) ModulationCCITT

- (UInt16) ModulationScheme

- (字串) Name

- (字串) PNPDeviceID

- (字串) PortSubClass

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (字串) Prefix

- (字串) Properties

- (字串) ProviderName

- (字串) Pulse

- (字串) Reset

- (字串) ResponsesKeyName

- (UInt8) RingsBeforeAnswer

- (字串) SpeakerModeDial

- (字串) SpeakerModeOff

- (字串) SpeakerModeOn

- (字串) SpeakerModeSetup

- (字串) SpeakerVolumeHigh

- (UInt16) SpeakerVolumeInfo

- (字串) SpeakerVolumeLow

- (字串) SpeakerVolumeMed

- (字串) Status

- (UInt16) StatusInfo

- (字串) StringFormat

- (布林值) SupportsCallback

- (布林值) SupportsSynchronousConnect

- (字串) SystemName

- (字串) Terminator

- (日期時間) TimeOfLastReset

- (字串) Tone

- (字串) VoiceSwitchFeature



## <a name="motherboard"></a>主機板

命名空間：root\cimv2

類別 Win32_MotherboardDevice


- (字串) DeviceID

- (UInt16) Availability

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (字串) Name

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (字串) PrimaryBusType

- (字串) RevisionNumber

- (字串) SecondaryBusType

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName


## <a name="nap-client"></a>NAP 用戶端

命名空間：root\Nap

類別 NAP_Client


- (字串) name

- (字串) description

- (字串) fixupURL

- (布林值) napEnabled

- (字串) napProtocolVersion

- (字串) probationTime

- (UInt32) systemIsolationState



## <a name="nap-system-health-agent"></a>NAP 系統健全狀況代理程式

命名空間：root\Nap

類別 NAP_SystemHealthAgent


- (UInt32) ID

- (字串) description

- (UInt32) fixupState

- (字串) friendlyName

- (字串) infoClsid

- (布林值) isBound

- (UInt8) percentage

- (字串) registrationDate

- (字串) vendorName

- (字串) version



## <a name="network-adapter"></a>網路介面卡

命名空間：root\cimv2

類別 Win32_NetworkAdapter


- (字串) DeviceID

- (字串) AdapterType

- (布林值) AutoSense

- (UInt16) Availability

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (UInt32) Index

- (日期時間) InstallDate

- (布林值) Installed

- (UInt32) LastErrorCode

- (字串) MACAddress

- (字串) Manufacturer

- (UInt32) MaxNumberControlled

- (UInt64) MaxSpeed

- (字串) Name

- (字串) NetworkAddresses[]

- (字串) PermanentAddress

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (字串) ProductName

- (字串) ServiceName

- (UInt64) Speed

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (日期時間) TimeOfLastReset



## <a name="network-adapter-configuration"></a>網路介面卡設定

命名空間：root\cimv2

類別 Win32_NetworkAdapterConfiguration


- (UInt32) Index

- (布林值) ArpAlwaysSourceRoute

- (布林值) ArpUseEtherSNAP

- (字串) Caption

- (字串) DatabasePath

- (布林值) DeadGWDetectEnabled

- (字串) DefaultIPGateway[]

- (UInt8) DefaultTOS

- (UInt8) DefaultTTL

- (字串) Description

- (布林值) DHCPEnabled

- (日期時間) DHCPLeaseExpires

- (日期時間) DHCPLeaseObtained

- (字串) DHCPServer

- (字串) DNSDomain

- (字串) DNSDomainSuffixSearchOrder[]

- (布林值) DNSEnabledForWINSResolution

- (字串) DNSHostName

- (字串) DNSServerSearchOrder[]

- (布林值) DomainDNSRegistrationEnabled

- (UInt32) ForwardBufferMemory

- (布林值) FullDNSRegistrationEnabled

- (UInt16) GatewayCostMetric[]

- (UInt8) IGMPLevel

- (字串) IPAddress[]

- (UInt32) IPConnectionMetric

- (布林值) IPEnabled

- (布林值) IPFilterSecurityEnabled

- (布林值) IPPortSecurityEnabled

- (字串) IPSecPermitIPProtocols[]

- (字串) IPSecPermitTCPPorts[]

- (字串) IPSecPermitUDPPorts[]

- (字串) IPSubnet[]

- (布林值) IPUseZeroBroadcast

- (字串) IPXAddress

- (布林值) IPXEnabled

- (字串) IPXFrameType

- (UInt32) IPXMediaType

- (字串) IPXNetworkNumber[]

- (字串) IPXVirtualNetNumber

- (UInt32) KeepAliveInterval

- (UInt32) KeepAliveTime

- (字串) MACAddress

- (UInt32) MTU

- (UInt32) NumForwardPackets

- (布林值) PMTUBHDetectEnabled

- (布林值) PMTUDiscoveryEnabled

- (字串) ServiceName

- (字串) SettingID

- (UInt32) TcpipNetbiosOptions

- (UInt32) TcpMaxConnectRetransmissions

- (UInt32) TcpMaxDataRetransmissions

- (UInt32) TcpNumConnections

- (布林值) TcpUseRFC1122UrgentPointer

- (UInt16) TcpWindowSize

- (布林值) WINSEnableLMHostsLookup

- (字串) WINSHostLookupFile

- (字串) WINSPrimaryServer

- (字串) WINSScopeID

- (字串) WINSSecondaryServer



## <a name="network-client"></a>網路用戶端

命名空間：root\cimv2

類別 Win32_NetworkClient


- (字串) Name

- (字串) Caption

- (字串) Description

- (日期時間) InstallDate

- (字串) Manufacturer

- (字串) Status



## <a name="network-login-profile"></a>網路登入設定檔

命名空間：root\cimv2

類別 Win32_NetworkLoginProfile


- (字串) Name

- (日期時間) AccountExpires

- (UInt32) AuthorizationFlags

- (UInt32) BadPasswordCount

- (字串) Caption

- (UInt32) CodePage

- (字串) Comment

- (UInt32) CountryCode

- (字串) Description

- (UInt32) Flags

- (字串) FullName

- (字串) HomeDirectory

- (字串) HomeDirectoryDrive

- (日期時間) LastLogoff

- (日期時間) LastLogon

- (字串) LogonHours

- (字串) LogonServer

- (UInt64) MaximumStorage

- (UInt32) NumberOfLogons

- (字串) Parameters

- (日期時間) PasswordAge

- (日期時間) PasswordExpires

- (UInt32) PrimaryGroupId

- (UInt32) Privileges

- (字串) Profile

- (字串) ScriptPath

- (字串) SettingID

- (UInt32) UnitsPerWeek

- (字串) UserComment

- (UInt32) UserId

- (字串) UserType

- (字串) Workstations



## <a name="nt-eventlog-file"></a>NT Eventlog 檔案

命名空間：root\cimv2

類別 Win32_NTEventlogFile


- (字串) Name

- (UInt32) AccessMask

- (布林值) Archive

- (字串) Caption

- (布林值) Compressed

- (字串) CompressionMethod

- (日期時間) CreationDate

- (字串) Description

- (字串) Drive

- (字串) EightDotThreeFileName

- (布林值) Encrypted

- (字串) EncryptionMethod

- (字串) Extension

- (字串) FileName

- (UInt64) FileSize

- (字串) FileType

- (字串) FSName

- (布林值) Hidden

- (日期時間) InstallDate

- (UInt64) InUseCount

- (日期時間) LastAccessed

- (日期時間) LastModified

- (字串) LogfileName

- (字串) Manufacturer

- (UInt32) MaxFileSize

- (UInt32) NumberOfRecords

- (UInt32) OverwriteOutDated

- (字串) OverWritePolicy

- (字串) Path

- (布林值) Readable

- (字串) Sources[]

- (字串) Status

- (布林值) System

- (字串) Version

- (布林值) Writeable



## <a name="office365proplusconfigurations"></a>Office365ProPlusConfigurations

命名空間：root\cimv2

類別 Office365ProPlusConfigurations


- (字串) KeyName

- (字串) AutoUpgrade

- (字串) CCMManaged

- (字串) CDNBaseUrl

- (字串) cfgUpdateChannel

- (字串) ClientCulture

- (字串) ClientFolder

- (字串) GPOChannel

- (字串) GPOOfficeMgmtCOM

- (字串) InstallationPath

- (字串) LastScenario

- (字串) LastScenarioResult

- (字串) OfficeMgmtCOM

- (字串) Platform

- (字串) SharedComputerLicensing

- (字串) UpdateChannel

- (字串) UpdatePath

- (字串) UpdatesEnabled

- (字串) UpdateUrl

- (字串) VersionToReport



## <a name="office-addin"></a>Office 增益集

命名空間：root\ccm\InvAgt

類別 CCM_OfficeAddin


- (字串) Architecture

- (字串) ID

- (字串) OfficeApp

- (字串) Type

- (UInt32) AverageLoadTimeInMilliseconds

- (字串) CLSID

- (字串) CompanyName

- (UInt32) CrashCount

- (字串) Description

- (UInt32) ErrorCount

- (字串) FileName

- (UInt64) FileSize

- (UInt32) FileTimestamp

- (字串) FileVersion

- (字串) FriendlyName

- (字串) FriendlyNameHash

- (字串) IdHash

- (UInt32) LoadBehavior

- (UInt32) LoadCount

- (UInt32) LoadFailCount

- (字串) ProductName

- (字串) ProductVersion



## <a name="office-client-metric"></a>Office 用戶端度量

命名空間：root\ccm\InvAgt

類別 CCM_OfficeClientMetric


- (字串) OfficeApp

- (UInt32) CompatibilityErrorCount

- (UInt32) CrashedSessionCount

- (UInt32) MacroCompileErrorCount

- (UInt32) MacroRuntimeErrorCount

- (UInt32) SessionCount



## <a name="office-device-summary"></a>Office 裝置摘要

命名空間：root\ccm\InvAgt

類別 CCM_OfficeDeviceSummary


- (布林值) IsProPlusInstalled

- (布林值) IsTelemetryEnabled



## <a name="office-document-metric"></a>Office 文件度量

命名空間：root\ccm\InvAgt

類別 CCM_OfficeDocumentMetric


- (字串) OfficeApp

- (UInt32) TotalCloudDocs

- (UInt32) TotalLegacyDocs

- (UInt32) TotalLocalDocs

- (UInt32) TotalMacroDocs

- (UInt32) TotalNonMacroDocs

- (UInt32) TotalUncDocs



## <a name="office-document-solution"></a>Office 文件解決方案

命名空間：root\ccm\InvAgt

類別 CCM_OfficeDocumentSolution


- (字串) DocumentSolutionId

- (字串) OfficeApp

- (UInt32) CompatibilityErrorCount

- (UInt32) CrashCount

- (字串) ExampleFileName

- (UInt32) LoadCount

- (UInt32) LoadFailCount

- (UInt32) MacroCompileErrorCount

- (UInt32) MacroRuntimeErrorCount

- (字串) Type



## <a name="office-macro-error"></a>Office 巨集錯誤

命名空間：root\ccm\InvAgt

類別 CCM_OfficeMacroError


- (字串) DocumentSolutionId

- (UInt32) ErrorCode

- (UInt32) Count

- (UInt64) LastOccurrence

- (字串) Type



## <a name="office-product-info"></a>Office 產品資訊

命名空間：root\ccm\InvAgt

類別 CCM_OfficeProductInfo


- (字串) ProductName

- (字串) ProductVersion

- (字串) Architecture

- (字串) Channel

- (UInt32) IsProPlusInstalled

- (字串) Language

- (字串) LicenseState



## <a name="office-vba-rule-violation"></a>違反 Office VBA 規則

命名空間：root\ccm\InvAgt

類別 CCM_OfficeVbaRuleViolation


- (UInt32) RuleId

- (UInt32) FileCount

- (字串) OfficeApp



## <a name="office-vbasummary"></a>Office VBA 摘要

命名空間：root\ccm\InvAgt

類別 CCM_OfficeVbaScanResultsSummary


- (UInt32) Design

- (UInt32) Design64

- (UInt32) DuplicateVba

- (布林值) HasResults

- (UInt32) HasVba

- (UInt32) Inaccessible

- (UInt32) Issues

- (UInt32) Issues64

- (UInt32) IssuesNone

- (UInt32) IssuesNone64

- (UInt32) Locked

- (UInt32) NoVba

- (UInt32) Protected

- (UInt32) RemLimited

- (UInt32) RemLimited64

- (UInt32) RemSignificant

- (UInt32) RemSignificant64

- (UInt32) Score

- (UInt32) Score64

- (UInt32) Total

- (UInt32) Validation

- (UInt32) Validation64



## <a name="operating-system"></a>作業系統

命名空間：root\cimv2

類別 Win32_OperatingSystem


- (字串) Name

- (字串) BootDevice

- (字串) BuildNumber

- (字串) BuildType

- (字串) Caption

- (字串) CodeSet

- (字串) CountryCode

- (字串) CSDVersion

- (SInt16) CurrentTimeZone

- (布林值) Debug

- (字串) Description

- (布林值) Distributed

- (UInt8) ForegroundApplicationBoost

- (UInt64) FreePhysicalMemory

- (UInt64) FreeSpaceInPagingFiles

- (UInt64) FreeVirtualMemory

- (日期時間) InstallDate

- (日期時間) LastBootUpTime

- (日期時間) LocalDateTime

- (字串) Locale

- (字串) Manufacturer

- (UInt32) MaxNumberOfProcesses

- (UInt64) MaxProcessMemorySize

- (字串) MUILanguages[]

- (UInt32) NumberOfLicensedUsers

- (UInt32) NumberOfProcesses

- (UInt32) NumberOfUsers

- (UInt32) OperatingSystemSKU

- (字串) Organization

- (字串) OSArchitecture

- (UInt32) OSLanguage

- (UInt32) OSProductSuite

- (UInt16) OSType

- (字串) OtherTypeDescription

- (字串) PlusProductID

- (字串) PlusVersionNumber

- (布林值) Primary

- (UInt32) ProductType

- (字串) RegisteredUser

- (字串) SerialNumber

- (UInt16) ServicePackMajorVersion

- (UInt16) ServicePackMinorVersion

- (UInt64) SizeStoredInPagingFiles

- (字串) Status

- (字串) SystemDevice

- (字串) SystemDirectory

- (UInt64) TotalSwapSpaceSize

- (UInt64) TotalVirtualMemorySize

- (UInt64) TotalVisibleMemorySize

- (字串) Version

- (字串) WindowsDirectory



## <a name="operating-system-ex"></a>作業系統 EX

命名空間：root\cimv2

類別 CCM_OperatingSystemExtended


- (字串) Name

- (UInt32) SKU



## <a name="operating-system-recovery-configuration"></a>作業系統復原設定

命名空間：root\cimv2

類別 Win32_OSRecoveryConfiguration


- (字串) Name

- (布林值) AutoReboot

- (字串) Caption

- (字串) DebugFilePath

- (字串) Description

- (布林值) KernelDumpOnly

- (布林值) OverwriteExistingDebugFile

- (布林值) SendAdminAlert

- (字串) SettingID

- (布林值) WriteDebugInfo

- (布林值) WriteToSystemLog



## <a name="optional-feature"></a>選用功能

命名空間：root\cimv2

類別 Win32_OptionalFeature


- (字串) Name

- (字串) Caption

- (字串) Description

- (日期時間) InstallDate

- (UInt32) InstallState

- (字串) Status



## <a name="page-file-setting"></a>分頁檔案設定

命名空間：root\cimv2

類別 Win32_PageFileSetting


- (字串) Name

- (字串) Caption

- (字串) Description

- (UInt32) InitialSize

- (UInt32) MaximumSize

- (字串) SettingID



## <a name="parallel-port"></a>平行埠

命名空間：root\cimv2

類別 Win32_ParallelPort


- (字串) DeviceID

- (UInt16) Availability

- (UInt16) Capabilities[]

- (字串) CapabilityDescriptions[]

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (布林值) DMASupport

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (UInt32) MaxNumberControlled

- (字串) Name

- (布林值) OSAutoDiscovered

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (日期時間) TimeOfLastReset



## <a name="bios"></a>BIOS

命名空間：root\cimv2

類別 Win32_BIOS


- (字串) Name

- (字串) SoftwareElementID

- (UInt16) SoftwareElementState

- (UInt16) TargetOperatingSystem

- (字串) Version

- (UInt16) BiosCharacteristics[]

- (字串) BIOSVersion[]

- (字串) BuildNumber

- (字串) Caption

- (字串) CodeSet

- (字串) CurrentLanguage

- (字串) Description

- (字串) IdentificationCode

- (UInt16) InstallableLanguages

- (日期時間) InstallDate

- (字串) LanguageEdition

- (字串) ListOfLanguages[]

- (字串) Manufacturer

- (字串) OtherTargetOS

- (布林值) PrimaryBIOS

- (日期時間) ReleaseDate

- (字串) SerialNumber

- (字串) SMBIOSBIOSVersion

- (UInt16) SMBIOSMajorVersion

- (UInt16) SMBIOSMinorVersion

- (布林值) SMBIOSPresent

- (字串) Status



## <a name="pcmcia-controller"></a>PCMCIA 控制器

命名空間：root\cimv2

類別 Win32_PCMCIAController


- (字串) DeviceID

- (UInt16) Availability

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (字串) Manufacturer

- (UInt32) MaxNumberControlled

- (字串) Name

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (日期時間) TimeOfLastReset



## <a name="physical-memory"></a>實體記憶體

命名空間：root\cimv2

類別 Win32_PhysicalMemory


- (字串) CreationClassName

- (字串) Tag

- (字串) BankLabel

- (UInt64) Capacity

- (字串) Caption

- (UInt16) DataWidth

- (字串) Description

- (字串) DeviceLocator

- (UInt16) FormFactor

- (布林值) HotSwappable

- (日期時間) InstallDate

- (UInt16) InterleaveDataDepth

- (UInt32) InterleavePosition

- (字串) Manufacturer

- (UInt16) MemoryType

- (字串) Model

- (字串) Name

- (字串) OtherIdentifyingInfo

- (字串) PartNumber

- (UInt32) PositionInRow

- (布林值) PoweredOn

- (布林值) Removable

- (布林值) Replaceable

- (字串) SerialNumber

- (字串) SKU

- (UInt32) Speed

- (字串) Status

- (UInt16) TotalWidth

- (UInt16) TypeDetail

- (字串) Version



## <a name="physicaldisk"></a>PhysicalDisk

命名空間：root\microsoft\windows\storage

類別 MSFT_PhysicalDisk


- (字串) ObjectId

- (UInt64) AllocatedSize

- (UInt16) BusType

- (UInt16) CannotPoolReason[]

- (布林值) CanPool

- (字串) Description

- (字串) DeviceId

- (UInt16) EnclosureNumber

- (字串) FirmwareVersion

- (字串) FriendlyName

- (UInt16) HealthStatus

- (布林值) IsIndicationEnabled

- (布林值) IsPartial

- (UInt64) LogicalSectorSize

- (字串) Manufacturer

- (UInt16) MediaType

- (字串) Model

- (UInt16) OperationalStatus[]

- (字串) OtherCannotPoolReasonDescription

- (字串) PartNumber

- (字串) PhysicalLocation

- (UInt64) PhysicalSectorSize

- (字串) SerialNumber

- (UInt64) Size

- (UInt16) SlotNumber

- (字串) SoftwareVersion

- (UInt32) SpindleSpeed

- (UInt16) SupportedUsages[]

- (字串) UniqueId

- (UInt16) Usage



## <a name="pnp-device-driver"></a>PNP 裝置驅動程式

命名空間：root\cimv2

類別 Win32_PnpEntity


- (字串) DeviceID

- (UInt16) Availability

- (字串) Caption

- (字串) ClassGuid

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) CreationClassName

- (字串) Description

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (字串) Manufacturer

- (字串) Name

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (字串) Service

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemCreationClassName

- (字串) SystemName



## <a name="pointing-device"></a>指標裝置

命名空間：root\cimv2

類別 Win32_PointingDevice


- (字串) DeviceID

- (UInt16) Availability

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (UInt16) DeviceInterface

- (UInt32) DoubleSpeedThreshold

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (UInt16) Handedness

- (字串) HardwareType

- (字串) InfFileName

- (字串) InfSection

- (日期時間) InstallDate

- (布林值) IsLocked

- (UInt32) LastErrorCode

- (字串) Manufacturer

- (字串) Name

- (UInt8) NumberOfButtons

- (字串) PNPDeviceID

- (UInt16) PointingType

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt32) QuadSpeedThreshold

- (UInt32) Resolution

- (UInt32) SampleRate

- (字串) Status

- (UInt16) StatusInfo

- (UInt32) Synch

- (字串) SystemName



## <a name="portable-battery"></a>可攜式電池

命名空間：root\cimv2

類別 Win32_PortableBattery


- (字串) DeviceID

- (UInt16) Availability

- (UInt16) BatteryStatus

- (UInt16) CapacityMultiplier

- (字串) Caption

- (UInt16) Chemistry

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (UInt32) DesignCapacity

- (UInt64) DesignVoltage

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (UInt16) EstimatedChargeRemaining

- (UInt32) EstimatedRunTime

- (UInt32) ExpectedLife

- (UInt32) FullChargeCapacity

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (字串) Location

- (字串) ManufactureDate

- (字串) Manufacturer

- (UInt16) MaxBatteryError

- (UInt32) MaxRechargeTime

- (字串) Name

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (字串) SmartBatteryVersion

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (UInt32) TimeOnBattery

- (UInt32) TimeToFullCharge



## <a name="ports"></a>連接埠

命名空間：root\cimv2

類別 Win32_PortResource

- (UInt64) StartingAddress

- (布林值) Alias

- (字串) Caption

- (字串) Description

- (UInt64) EndingAddress

- (日期時間) InstallDate

- (字串) Name

- (字串) Status



## <a name="power-capabilities"></a>電池容量

命名空間：root\CCM\powermanagementagent

類別 CCM_PwrMgmtSystemPowerCapabilities


- (UInt32) PreferredPMProfile

- (布林值) ApmPresent

- (布林值) BatteriesAreShortTerm

- (布林值) FullWake

- (布林值) LidPresent

- (字串) MinDeviceWakeState

- (布林值) ProcessorThrottle

- (字串) RtcWake

- (布林值) SystemBatteriesPresent

- (布林值) SystemS1

- (布林值) SystemS2

- (布林值) SystemS3

- (布林值) SystemS4

- (布林值) SystemS5

- (布林值) UpsPresent

- (布林值) VideoDimPresent



## <a name="power-configurations"></a>電源設定

命名空間：root\CCM\policy\machine\actualconfig

類別 CCM_PowerConfig


- (字串) PowerConfigID

- (UInt32) DurationInSec

- (字串) NonPeakPowerPlan

- (字串) NonPeakPowerPlanName

- (字串) PeakPowerPlan

- (字串) PeakPowerPlanName

- (字串) PeakStartTimeHoursMin

- (字串) WakeUpTimeHoursMin



## <a name="power-management-insomnia-reasons"></a>電源管理無法休眠的原因

命名空間：root\CCM\powermanagementagent

類別 CCM_PwrMgmtLastSuspendError


- (字串) Requester

- (字串) RequesterType

- (字串) RequestType

- (日期時間) Time

- (UInt32) AdditionalCode

- (字串) AdditionalInfo

- (字串) RequesterInfo

- (布林值) UnknownRequester



## <a name="power-management-daily"></a>每日電源管理

命名空間：root\CCM\powermanagementagent

類別 CCM_PwrMgmtActualDay


- (日期時間) Date

- (字串) TypeOfEvent

- (UInt32) hr0_1

- (UInt32) hr1_2

- (UInt32) hr10_11

- (UInt32) hr11_12

- (UInt32) hr12_13

- (UInt32) hr13_14

- (UInt32) hr14_15

- (UInt32) hr15_16

- (UInt32) hr16_17

- (UInt32) hr17_18

- (UInt32) hr18_19

- (UInt32) hr19_20

- (UInt32) hr2_3

- (UInt32) hr20_21

- (UInt32) hr21_22

- (UInt32) hr22_23

- (UInt32) hr23_0

- (UInt32) hr3_4

- (UInt32) hr4_5

- (UInt32) hr5_6

- (UInt32) hr6_7

- (UInt32) hr7_8

- (UInt32) hr8_9

- (UInt32) hr9_10

- (UInt32) minutesTotal



## <a name="power-client-opt-out-settings"></a>電源用戶端選擇不要設定

命名空間：root\ccm\ClientSDK

類別 CCM_PowerManagementClientOptoutSetting


- (布林值) AdminAllowOptout

- (布林值) EffectiveClientOptOut

- (布林值) IsClientOptOut



## <a name="power-management-monthly"></a>每月電源管理

命名空間：root\CCM\powermanagementagent

類別 CCM_PwrMgmtMonth


- (日期時間) MonthStart

- (UInt32) minutesComputerActive

- (UInt32) minutesComputerOn

- (UInt32) minutesComputerShutdown

- (UInt32) minutesComputerSleep

- (UInt32) minutesMonitorOn

- (UInt32) minutesTotal

- (字串) TypeOfEvent



## <a name="power-settings"></a>電源設定

命名空間：root\cimv2\sms

類別 SMS_PowerSettings


- (字串) GUID

- (字串) ACSettingIndex

- (字串) ACValue

- (字串) DCSettingIndex

- (字串) DCValue

- (字串) Name

- (字串) UnitSpecifier



## <a name="print-jobs"></a>列印工作

命名空間：root\cimv2

類別 Win32_PrintJob


- (字串) Name

- (字串) Caption

- (字串) DataType

- (字串) Description

- (字串) Document

- (字串) DriverName

- (日期時間) ElapsedTime

- (字串) HostPrintQueue

- (日期時間) InstallDate

- (UInt32) JobId

- (字串) JobStatus

- (字串) Notify

- (字串) Owner

- (UInt32) PagesPrinted

- (字串) Parameters

- (字串) PrintProcessor

- (UInt32) Priority

- (UInt32) Size

- (日期時間) StartTime

- (字串) Status

- (UInt32) StatusMask

- (日期時間) TimeSubmitted

- (UInt32) TotalPages

- (日期時間) UntilTime



## <a name="printer-configuration"></a>印表機設定

命名空間：root\cimv2

類別 Win32_PrinterConfiguration


- (字串) Name

- (UInt32) BitsPerPel

- (字串) Caption

- (布林值) Collate

- (UInt32) Color

- (UInt32) Copies

- (字串) Description

- (字串) DeviceName

- (UInt32) DisplayFlags

- (UInt32) DisplayFrequency

- (UInt32) DitherType

- (UInt32) DriverVersion

- (布林值) Duplex

- (字串) FormName

- (UInt32) HorizontalResolution

- (UInt32) ICMIntent

- (UInt32) ICMMethod

- (UInt32) LogPixels

- (UInt32) MediaType

- (UInt32) Orientation

- (UInt32) PaperLength

- (字串) PaperSize

- (UInt32) PaperWidth

- (UInt32) PelsHeight

- (UInt32) PelsWidth

- (UInt32) PrintQuality

- (UInt32) Scale

- (字串) SettingID

- (UInt32) SpecificationVersion

- (UInt32) TTOption

- (UInt32) VerticalResolution

- (UInt32) XResolution

- (UInt32) YResolution



## <a name="printer-device"></a>印表機裝置

命名空間：root\cimv2

類別 Win32_Printer


- (字串) DeviceID

- (UInt32) Attributes

- (UInt16) Availability

- (UInt32) AveragePagesPerMinute

- (UInt16) Capabilities[]

- (字串) CapabilityDescriptions[]

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (UInt32) DefaultPriority

- (字串) Description

- (UInt16) DetectedErrorState

- (字串) DriverName

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (UInt32) HorizontalResolution

- (日期時間) InstallDate

- (UInt32) JobCountSinceLastReset

- (UInt16) LanguagesSupported[]

- (UInt32) LastErrorCode

- (字串) Location

- (字串) Name

- (UInt16) PaperSizesSupported[]

- (字串) PNPDeviceID

- (字串) PortName

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (字串) PrinterPaperNames[]

- (UInt32) PrinterState

- (UInt16) PrinterStatus

- (字串) PrintJobDataType

- (字串) PrintProcessor

- (字串) SeparatorFile

- (字串) ServerName

- (字串) ShareName

- (布林值) SpoolEnabled

- (日期時間) StartTime

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (日期時間) TimeOfLastReset

- (日期時間) UntilTime

- (UInt32) VerticalResolution



## <a name="process"></a>程序

命名空間：root\cimv2

類別 Win32_Process


- (字串) Handle

- (字串) Caption

- (日期時間) CreationDate

- (字串) Description

- (字串) ExecutablePath

- (UInt16) ExecutionState

- (UInt32) HandleCount

- (日期時間) InstallDate

- (UInt64) KernelModeTime

- (UInt32) MaximumWorkingSetSize

- (UInt32) MinimumWorkingSetSize

- (字串) Name

- (字串) OSName

- (UInt64) OtherOperationCount

- (UInt64) OtherTransferCount

- (UInt32) PageFaults

- (UInt32) PageFileUsage

- (UInt32) ParentProcessId

- (UInt32) PeakPageFileUsage

- (UInt64) PeakVirtualSize

- (UInt32) PeakWorkingSetSize

- (UInt32) Priority

- (UInt64) PrivatePageCount

- (UInt32) ProcessId

- (UInt32) QuotaNonPagedPoolUsage

- (UInt32) QuotaPagedPoolUsage

- (UInt32) QuotaPeakNonPagedPoolUsage

- (UInt32) QuotaPeakPagedPoolUsage

- (UInt64) ReadOperationCount

- (UInt64) ReadTransferCount

- (UInt32) SessionId

- (字串) Status

- (日期時間) TerminationDate

- (UInt32) ThreadCount

- (UInt64) UserModeTime

- (UInt64) VirtualSize

- (字串) WindowsVersion

- (UInt64) WorkingSetSize

- (UInt64) WriteOperationCount

- (UInt64) WriteTransferCount



## <a name="processor"></a>處理器

命名空間：root\cimv2\sms

類別 SMS_Processor


- (字串) DeviceID

- (UInt16) AddressWidth

- (UInt16) Architecture

- (UInt16) Availability

- (UInt16) BrandID

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) CPUHash

- (字串) CPUKey

- (UInt16) CpuStatus

- (UInt32) CurrentClockSpeed

- (UInt16) CurrentVoltage

- (UInt16) DataWidth

- (字串) Description

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (UInt32) ExtClock

- (UInt16) Family

- (日期時間) InstallDate

- (布林值) Is64Bit

- (布林值) IsHyperthreadCapable

- (布林值) IsHyperthreadEnabled

- (布林值) IsMobile

- (布林值) IsTrustedExecutionCapable

- (布林值) IsVitualizationCapable

- (UInt32) L2CacheSize

- (UInt32) L2CacheSpeed

- (UInt32) L3CacheSize

- (UInt32) L3CacheSpeed

- (UInt32) LastErrorCode

- (UInt16) Level

- (UInt16) LoadPercentage

- (字串) Manufacturer

- (UInt32) MaxClockSpeed

- (字串) Name

- (UInt32) NormSpeed

- (UInt32) NumberOfCores

- (UInt32) NumberOfLogicalProcessors

- (字串) OtherFamilyDescription

- (布林值) PartOfDomain

- (UInt32) PCache

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (字串) ProcessorId

- (UInt16) ProcessorType

- (UInt16) Revision

- (字串) Role

- (字串) SocketDesignation

- (字串) Status

- (UInt16) StatusInfo

- (字串) Stepping

- (字串) SystemName

- (字串) UniqueId

- (UInt16) UpgradeMethod

- (字串) Version

- (UInt32) VoltageCaps

- (字串) Workgroup



## <a name="protected-volume-information"></a>受保護的磁碟區資訊

命名空間：root\cimv2\sms

類別 CCM_ProtectedVolumeInfo


- (字串) Name

- (字串) DriveLetter

- (UInt32) ProtectionType



## <a name="protocol"></a>通訊協定

命名空間：root\cimv2

類別 Win32_NetworkProtocol


- (字串) Name

- (字串) Caption

- (布林值) ConnectionlessService

- (字串) Description

- (布林值) GuaranteesDelivery

- (布林值) GuaranteesSequencing

- (日期時間) InstallDate

- (UInt32) MaximumAddressSize

- (UInt32) MaximumMessageSize

- (布林值) MessageOriented

- (UInt32) MinimumAddressSize

- (布林值) PseudoStreamOriented

- (字串) Status

- (布林值) SupportsBroadcasting

- (布林值) SupportsConnectData

- (布林值) SupportsDisconnectData

- (布林值) SupportsEncryption

- (布林值) SupportsExpeditedData

- (布林值) SupportsFragmentation

- (布林值) SupportsGracefulClosing

- (布林值) SupportsGuaranteedBandwidth

- (布林值) SupportsMulticasting

- (布林值) SupportsQualityofService



## <a name="quick-fix-engineering"></a>快速檢修

命名空間：root\cimv2

類別 Win32_QuickFixEngineering


- (字串) HotFixID

- (字串) ServicePackInEffect

- (字串) Caption

- (字串) Description

- (字串) FixComments

- (日期時間) InstallDate

- (字串) InstalledBy

- (字串) InstalledOn

- (字串) Name

- (字串) Status



## <a name="ccm-recently-used-applications"></a>CCM 最近使用的應用程式

命名空間：root\cimv2\sms

類別 CCM_RecentlyUsedApps


- (字串) ExplorerFileName

- (字串) FolderPath

- (字串) LastUserName

- (字串) AdditionalProductCodes

- (字串) CompanyName

- (字串) FileDescription

- (字串) FilePropertiesHash

- (UInt32) FileSize

- (字串) FileVersion

- (日期時間) LastUsedTime

- (UInt32) LaunchCount

- (字串) msiDisplayName

- (字串) msiPublisher

- (字串) msiVersion

- (字串) OriginalFileName

- (字串) ProductCode

- (UInt32) ProductLanguage

- (字串) ProductName

- (字串) ProductVersion

- (字串) SoftwarePropertiesHash



## <a name="registry"></a>登錄

命名空間：root\cimv2

類別 Win32_Registry


- (字串) Name

- (字串) Caption

- (UInt32) CurrentSize

- (字串) Description

- (日期時間) InstallDate

- (UInt32) MaximumSize

- (UInt32) ProposedSize

- (字串) Status



## <a name="scsi-controller"></a>SCSI 控制器

命名空間：root\cimv2

類別 Win32_SCSIController


- (字串) DeviceID

- (UInt16) Availability

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (UInt32) ControllerTimeouts

- (字串) Description

- (字串) DeviceMap

- (字串) DriverName

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (字串) HardwareVersion

- (UInt32) Index

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (字串) Manufacturer

- (UInt32) MaxDataWidth

- (UInt32) MaxNumberControlled

- (UInt64) MaxTransferRate

- (字串) Name

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt16) ProtectionManagement

- (UInt16) ProtocolSupported

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (日期時間) TimeOfLastReset



## <a name="serial-port-configuration"></a>序列埠設定

命名空間：root\cimv2

類別 Win32_SerialPortConfiguration


- (字串) Name

- (布林值) AbortReadWriteOnError

- (UInt32) BaudRate

- (布林值) BinaryModeEnabled

- (UInt32) BitsPerByte

- (字串) Caption

- (布林值) ContinueXMitOnXOff

- (布林值) CTSOutflowControl

- (字串) Description

- (布林值) DiscardNULLBytes

- (布林值) DSROutflowControl

- (布林值) DSRSensitivity

- (字串) DTRFlowControlType

- (UInt32) EOFCharacter

- (UInt32) ErrorReplaceCharacter

- (布林值) ErrorReplacementEnabled

- (UInt32) EventCharacter

- (布林值) IsBusy

- (字串) Parity

- (布林值) ParityCheckEnabled

- (字串) RTSFlowControlType

- (字串) SettingID

- (字串) StopBits

- (UInt32) XOffCharacter

- (UInt32) XOffXMitThreshold

- (UInt32) XOnCharacter

- (UInt32) XOnXMitThreshold

- (UInt32) XOnXOffInFlowControl

- (UInt32) XOnXOffOutFlowControl



## <a name="serial-ports"></a>序列埠

命名空間：root\cimv2

類別 Win32_SerialPort


- (字串) DeviceID

- (UInt16) Availability

- (布林值) Binary

- (UInt16) Capabilities[]

- (字串) CapabilityDescriptions[]

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (UInt32) MaxBaudRate

- (UInt32) MaximumInputBufferSize

- (UInt32) MaximumOutputBufferSize

- (UInt32) MaxNumberControlled

- (字串) Name

- (布林值) OSAutoDiscovered

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (字串) ProviderType

- (布林值) SettableBaudRate

- (布林值) SettableDataBits

- (布林值) SettableFlowControl

- (布林值) SettableParity

- (布林值) SettableParityCheck

- (布林值) SettableRLSD

- (布林值) SettableStopBits

- (字串) Status

- (UInt16) StatusInfo

- (布林值) Supports16BitMode

- (布林值) SupportsDTRDSR

- (布林值) SupportsElapsedTimeouts

- (布林值) SupportsIntTimeouts

- (布林值) SupportsParityCheck

- (布林值) SupportsRLSD

- (布林值) SupportsRTSCTS

- (布林值) SupportsSpecialCharacters

- (布林值) SupportsXOnXOff

- (布林值) SupportsXOnXOffSet

- (字串) SystemName

- (日期時間) TimeOfLastReset



## <a name="server-feature"></a>伺服器功能

命名空間：root\cimv2

類別 Win32_ServerFeature


- (UInt32) ID

- (字串) Name

- (UInt32) ParentID



## <a name="services"></a>服務

命名空間：root\cimv2

類別 Win32_Service


- (字串) Name

- (布林值) AcceptPause

- (布林值) AcceptStop

- (字串) Caption

- (UInt32) CheckPoint

- (字串) Description

- (布林值) DesktopInteract

- (字串) DisplayName

- (字串) ErrorControl

- (UInt32) ExitCode

- (日期時間) InstallDate

- (字串) PathName

- (UInt32) ProcessId

- (UInt32) ServiceSpecificExitCode

- (字串) ServiceType

- (布林值) Started

- (字串) StartMode

- (字串) StartName

- (字串) State

- (字串) Status

- (字串) SystemName

- (UInt32) TagId

- (UInt32) WaitHint



## <a name="shares"></a>共用

命名空間：root\cimv2

類別 Win32_Share


- (字串) Name

- (UInt32) AccessMask

- (布林值) AllowMaximum

- (字串) Caption

- (字串) Description

- (日期時間) InstallDate

- (UInt32) MaximumAllowed

- (字串) Path

- (字串) Status

- (UInt32) Type



## <a name="sw-licensing-product"></a>SW 授權產品

命名空間：root\cimv2

類別 SoftwareLicensingProduct


- (字串) ID

- (字串) ApplicationID

- (字串) Description

- (日期時間) EvaluationEndDate

- (UInt32) GracePeriodRemaining

- (UInt32) LicenseStatus

- (字串) MachineURL

- (字串) Name

- (字串) OfflineInstallationId

- (字串) PartialProductKey

- (字串) ProcessorURL

- (字串) ProductKeyID

- (字串) ProductKeyURL

- (字串) UseLicenseURL



## <a name="sw-licensing-service"></a>SW 授權服務

命名空間：root\cimv2

類別 SoftwareLicensingService


- (字串) Version

- (字串) ClientMachineID

- (UInt32) IsKeyManagementServiceMachine

- (UInt32) KeyManagementServiceCurrentCount

- (字串) KeyManagementServiceMachine

- (字串) KeyManagementServiceProductKeyID

- (UInt32) PolicyCacheRefreshRequired

- (UInt32) RequiredClientCount

- (UInt32) VLActivationInterval

- (UInt32) VLRenewalInterval



## <a name="software-shortcut"></a>軟體捷徑

命名空間：root\cimv2\sms

類別 SMS_SoftwareShortcut


- (字串) ShortcutKey

- (字串) BinFileVersion

- (字串) BinProductVersion

- (字串) Description

- (字串) FilePropertiesHash

- (字串) FilePropertiesHashEx

- (UInt32) FileSize

- (字串) FileVersion

- (UInt32) Language

- (字串) ParentName

- (字串) Product

- (字串) ProductCode

- (字串) ProductVersion

- (字串) Publisher

- (字串) ShortcutName

- (UInt32) ShortcutType

- (字串) TargetExecutable



## <a name="sms_softwaretag"></a>SMS_SoftwareTag

命名空間：root\cimv2\sms

類別 SMS_SoftwareTag


- (字串) TagCreatorRegid

- (字串) UniqueID

- (字串) DisplayVersion

- (布林值) EntitlementRequired

- (字串) ProductName

- (字串) SoftwareCreator

- (字串) SoftwareCreatorRegid

- (字串) SoftwareLicensor

- (字串) SoftwareLicensorRegid

- (字串) TagCreator

- (SInt32) VersionMajor

- (SInt32) VersionMinor



## <a name="sound-devices"></a>音效裝置

命名空間：root\cimv2

類別 Win32_SoundDevice


- (字串) DeviceID

- (UInt16) Availability

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (UInt16) DMABufferSize

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (字串) Manufacturer

- (UInt32) MPU401Address

- (字串) Name

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (字串) ProductName

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName



## <a name="system-account"></a>系統帳戶

命名空間：root\cimv2

類別 Win32_SystemAccount


- (字串) Domain

- (字串) Name

- (字串) Caption

- (字串) Description

- (日期時間) InstallDate

- (字串) SID

- (UInt8) SIDType

- (字串) Status



## <a name="system-boot-data"></a>系統開機資料

命名空間：root\CCM

類別 CCM_SystemBootData


- (UInt64) SystemStartTime

- (UInt32) BiosDuration

- (UInt16) BootDiskMediaType

- (UInt32) BootDuration

- (UInt32) EventLogStart

- (UInt32) GPDuration

- (字串) OSVersion

- (UInt32) UpdateDuration



## <a name="system-boot-summary"></a>系統開機摘要

命名空間：root\CCM

類別 CCM_SystemBootSummary


- (UInt32) AverageBootFrequency

- (UInt32) LatestBiosDuration

- (UInt32) LatestBootDuration

- (UInt32) LatestCoreBootDuration

- (UInt32) LatestEventLogStart

- (UInt32) LatestGPDuration

- (UInt32) LatestUpdateDuration

- (UInt32) MaxBiosDuration

- (UInt32) MaxBootDuration

- (UInt32) MaxCoreBootDuration

- (UInt32) MaxEventLogStart

- (UInt32) MaxGPDuration

- (UInt32) MaxUpdateDuration

- (UInt32) MedianBiosDuration

- (UInt32) MedianBootDuration

- (UInt32) MedianCoreBootDuration

- (UInt32) MedianEventLogStart

- (UInt32) MedianGPDuration

- (UInt32) MedianUpdateDuration



## <a name="system-console-usage"></a>系統主控台使用方式

命名空間：root\cimv2\sms

類別 SMS_SystemConsoleUsage


- (日期時間) SecurityLogStartDate

- (字串) TopConsoleUser

- (UInt32) TotalConsoleTime

- (UInt32) TotalConsoleUsers

- (UInt32) TotalSecurityLogTime



## <a name="system-console-user"></a>系統主控台使用者

命名空間：root\cimv2\sms

類別 SMS_SystemConsoleUser


- (字串) SystemConsoleUser

- (日期時間) LastConsoleUse

- (UInt32) NumberOfConsoleLogons

- (UInt32) TotalUserConsoleMinutes



## <a name="system-devices"></a>系統裝置

命名空間：root\cimv2\sms

類別 CCM_SystemDevices


- (字串) Name

- (字串) CompatibleIDs[]

- (字串) DeviceID

- (字串) HardwareIDs[]

- (布林值) IsPnP



## <a name="system-drivers"></a>系統驅動程式

命名空間：root\cimv2

類別 Win32_SystemDriver


- (字串) Name

- (布林值) AcceptPause

- (布林值) AcceptStop

- (字串) Caption

- (字串) Description

- (布林值) DesktopInteract

- (字串) DisplayName

- (字串) ErrorControl

- (UInt32) ExitCode

- (日期時間) InstallDate

- (字串) PathName

- (UInt32) ServiceSpecificExitCode

- (字串) ServiceType

- (布林值) Started

- (字串) StartMode

- (字串) StartName

- (字串) State

- (字串) Status

- (字串) SystemName

- (UInt32) TagId



## <a name="system-enclosure"></a>系統機殼

命名空間：root\cimv2

類別 Win32_SystemEnclosure


- (字串) Tag

- (布林值) AudibleAlarm

- (字串) BreachDescription

- (字串) CableManagementStrategy

- (字串) Caption

- (UInt16) ChassisTypes[]

- (SInt16) CurrentRequiredOrProduced

- (字串) Description

- (UInt16) HeatGeneration

- (布林值) HotSwappable

- (日期時間) InstallDate

- (布林值) LockPresent

- (字串) Manufacturer

- (字串) Model

- (字串) Name

- (UInt16) NumberOfPowerCords

- (字串) OtherIdentifyingInfo

- (字串) PartNumber

- (布林值) PoweredOn

- (布林值) Removable

- (布林值) Replaceable

- (UInt16) SecurityBreach

- (UInt16) SecurityStatus

- (字串) SerialNumber

- (字串) ServiceDescriptions[]

- (UInt16) ServicePhilosophy[]

- (字串) SKU

- (字串) SMBIOSAssetTag

- (字串) Status

- (字串) TypeDescriptions[]

- (字串) Version

- (布林值) VisibleAlarm



## <a name="tape-drive"></a>磁帶機

命名空間：root\cimv2

類別 Win32_TapeDrive


- (字串) DeviceID

- (UInt16) Availability

- (UInt16) Capabilities[]

- (字串) CapabilityDescriptions[]

- (字串) Caption

- (UInt32) Compression

- (字串) CompressionMethod

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (UInt64) DefaultBlockSize

- (字串) Description

- (UInt32) ECC

- (UInt32) EOTWarningZoneSize

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (字串) ErrorMethodology

- (UInt32) FeaturesHigh

- (UInt32) FeaturesLow

- (字串) ID

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (字串) Manufacturer

- (UInt64) MaxBlockSize

- (UInt64) MaxMediaSize

- (UInt32) MaxPartitionCount

- (字串) MediaType

- (UInt64) MinBlockSize

- (字串) Name

- (布林值) NeedsCleaning

- (UInt32) NumberOfMediaSupported

- (UInt32) Padding

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt32) ReportSetMarks

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName



## <a name="time-zone"></a>時區

命名空間：root\cimv2

類別 Win32_TimeZone


- (字串) StandardName

- (SInt32) Bias

- (字串) Caption

- (SInt32) DaylightBias

- (UInt32) DaylightDay

- (UInt8) DaylightDayOfWeek

- (UInt32) DaylightHour

- (UInt32) DaylightMillisecond

- (UInt32) DaylightMinute

- (UInt32) DaylightMonth

- (字串) DaylightName

- (UInt32) DaylightSecond

- (UInt32) DaylightYear

- (字串) Description

- (字串) SettingID

- (UInt32) StandardBias

- (UInt32) StandardDay

- (UInt8) StandardDayOfWeek

- (UInt32) StandardHour

- (UInt32) StandardMillisecond

- (UInt32) StandardMinute

- (UInt32) StandardMonth

- (UInt32) StandardSecond

- (UInt32) StandardYear



## <a name="tpm"></a>TPM

命名空間：root\CIMv2\Security\MicrosoftTpm

類別 Win32_Tpm


- (布林值) IsActivated_InitialValue

- (布林值) IsEnabled_InitialValue

- (布林值) IsOwned_InitialValue

- (UInt32) ManufacturerId

- (字串) ManufacturerVersion

- (字串) ManufacturerVersionInfo

- (字串) PhysicalPresenceVersionInfo

- (字串) SpecVersion



## <a name="tpm-status"></a>TPM 狀態

命名空間：root\cimv2\sms

類別 SMS_TPM


- (布林值) IsReady

- (UInt32) Information

- (布林值) IsApplicable



## <a name="ts-issued-license"></a>TS 核發的授權

命名空間：root\cimv2

類別 Win32_TSIssuedLicense


- (UInt32) LicenseId

- (日期時間) ExpirationDate

- (日期時間) IssueDate

- (UInt32) KeyPackId

- (UInt32) LicenseStatus

- (字串) sHardwareId

- (字串) sIssuedToComputer

- (字串) sIssuedToUser



## <a name="ts-license-key-pack"></a>TS 授權金鑰包

命名空間：root\cimv2

類別 Win32_TSLicenseKeyPack


- (UInt32) KeyPackId

- (UInt32) AvailableLicenses

- (字串) Description

- (UInt32) IssuedLicenses

- (UInt32) KeyPackType

- (UInt32) ProductType

- (字串) ProductVersion

- (UInt32) TotalLicenses



## <a name="uninterruptible-power-supply"></a>不斷電供應系統

命名空間：root\cimv2

類別 Win32_UninterruptiblePowerSupply


- (字串) DeviceID

- (UInt16) ActiveInputVoltage

- (UInt16) Availability

- (布林值) BatteryInstalled

- (布林值) CanTurnOffRemotely

- (字串) Caption

- (字串) CommandFile

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (UInt16) EstimatedChargeRemaining

- (UInt32) EstimatedRunTime

- (UInt32) FirstMessageDelay

- (日期時間) InstallDate

- (布林值) IsSwitchingSupply

- (UInt32) LastErrorCode

- (布林值) LowBatterySignal

- (UInt32) MessageInterval

- (字串) Name

- (字串) PNPDeviceID

- (布林值) PowerFailSignal

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt32) Range1InputFrequencyHigh

- (UInt32) Range1InputFrequencyLow

- (UInt32) Range1InputVoltageHigh

- (UInt32) Range1InputVoltageLow

- (UInt32) Range2InputFrequencyHigh

- (UInt32) Range2InputFrequencyLow

- (UInt32) Range2InputVoltageHigh

- (UInt32) Range2InputVoltageLow

- (UInt16) RemainingCapacityStatus

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (UInt32) TimeOnBackup

- (UInt32) TotalOutputPower

- (UInt16) TypeOfRangeSwitching

- (字串) UPSPort



## <a name="usb-controller"></a>USB 控制器

命名空間：root\cimv2

類別 Win32_USBController


- (字串) DeviceID

- (UInt16) Availability

- (字串) Caption

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) Description

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (日期時間) InstallDate

- (UInt32) LastErrorCode

- (字串) Manufacturer

- (UInt32) MaxNumberControlled

- (字串) Name

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (日期時間) TimeOfLastReset



## <a name="usb-device"></a>USB 裝置

命名空間：root\cimv2

類別 Win32_USBDevice


- (字串) DeviceID

- (字串) Caption

- (字串) ClassGuid

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) CreationClassName

- (字串) Description

- (字串) Manufacturer

- (字串) Name

- (字串) PNPDeviceID

- (字串) Service

- (字串) Status

- (字串) SystemCreationClassName

- (字串) SystemName



## <a name="usm-user-profile"></a>USM 使用者設定檔

命名空間：root\cimv2

類別 Win32_UserProfile


- (字串) SID

- (UInt8) HealthStatus

- (字串) LastAttemptedProfileDownloadTime

- (字串) LastAttemptedProfileUploadTime

- (字串) LastBackgroundRegistryUploadTime

- (日期時間) LastDownloadTime

- (日期時間) LastUploadTime

- (日期時間) LastUseTime

- (布林值) Loaded

- (字串) LocalPath

- (UInt32) RefCount

- (布林值) RoamingConfigured

- (字串) RoamingPath

- (布林值) RoamingPreference

- (布林值) Special

- (UInt32) Status



## <a name="video-controller"></a>視訊控制卡

命名空間：root\cimv2

類別 Win32_VideoController


- (字串) DeviceID

- (UInt16) AcceleratorCapabilities[]

- (字串) AdapterCompatibility

- (字串) AdapterDACType

- (UInt32) AdapterRAM

- (UInt16) Availability

- (字串) CapabilityDescriptions[]

- (字串) Caption

- (UInt32) ColorTableEntries

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (UInt32) CurrentBitsPerPixel

- (UInt32) CurrentHorizontalResolution

- (UInt64) CurrentNumberOfColors

- (UInt32) CurrentNumberOfColumns

- (UInt32) CurrentNumberOfRows

- (UInt32) CurrentRefreshRate

- (UInt16) CurrentScanMode

- (UInt32) CurrentVerticalResolution

- (字串) Description

- (UInt32) DeviceSpecificPens

- (UInt32) DitherType

- (日期時間) DriverDate

- (字串) DriverVersion

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (UInt32) ICMIntent

- (UInt32) ICMMethod

- (字串) InfFilename

- (字串) InfSection

- (日期時間) InstallDate

- (字串) InstalledDisplayDrivers

- (UInt32) LastErrorCode

- (UInt32) MaxMemorySupported

- (UInt32) MaxNumberControlled

- (UInt32) MaxRefreshRate

- (UInt32) MinRefreshRate

- (布林值) Monochrome

- (字串) Name

- (UInt16) NumberOfColorPlanes

- (UInt32) NumberOfVideoPages

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (UInt32) ReservedSystemPaletteEntries

- (UInt32) SpecificationVersion

- (字串) Status

- (UInt16) StatusInfo

- (字串) SystemName

- (UInt32) SystemPaletteEntries

- (日期時間) TimeOfLastReset

- (UInt16) VideoArchitecture

- (UInt16) VideoMemoryType

- (UInt16) VideoMode

- (字串) VideoModeDescription

- (字串) VideoProcessor



## <a name="virtual-application-packages"></a>虛擬應用程式套件

命名空間：root\Microsoft\appvirt\client

類別 Package


- (字串) PackageGUID

- (UInt64) CachedLaunchSize

- (UInt16) CachedPercentage

- (UInt64) CachedSize

- (UInt64) LaunchSize

- (字串) Name

- (字串) SftPath

- (UInt64) TotalSize

- (字串) Version

- (字串) VersionGUID



## <a name="virtual-applications"></a>虛擬應用程式

命名空間：root\Microsoft\appvirt\client

類別 Application


- (字串) Name

- (字串) Version

- (字串) CachedOsdPath

- (UInt32) GlobalRunningCount

- (日期時間) LastLaunchOnSystem

- (布林值) Loading

- (字串) OriginalOsdPath

- (字串) PackageGUID



## <a name="virtual-machine-64"></a>虛擬機器 (64)

命名空間：root\cimv2

類別 Win32Reg_SMSGuestVirtualMachine64


- (字串) InstanceKey

- (字串) PhysicalHostName

- (字串) PhysicalHostNameFullyQualified



## <a name="virtual-machine"></a>虛擬機器

命名空間：root\cimv2

類別 Win32Reg_SMSGuestVirtualMachine


- (字串) InstanceKey

- (字串) PhysicalHostName

- (字串) PhysicalHostNameFullyQualified



## <a name="virtual-machine-details"></a>虛擬機器詳細資料

命名空間：root\vm\VirtualServer

類別 VirtualMachine


- (字串) Name

- (UInt32) CpuUtilization

- (UInt64) DiskBytesRead

- (UInt64) DiskBytesWritten

- (UInt64) DiskSpaceUsed

- (UInt64) HeartbeatCount

- (UInt32) HeartbeatInterval

- (UInt32) HeartbeatPercentage

- (UInt32) HeartbeatRate

- (UInt64) NetworkBytesReceived

- (UInt64) NetworkBytesSent

- (UInt64) PhysicalMemoryAllocated

- (UInt32) Uptime



## <a name="volume"></a>磁碟區

命名空間：root\cimv2

類別 Win32_Volume


- (字串) DeviceID

- (UInt16) Access

- (布林值) Automount

- (UInt16) Availability

- (UInt64) BlockSize

- (UInt64) Capacity

- (字串) Caption

- (布林值) Compressed

- (UInt32) ConfigManagerErrorCode

- (布林值) ConfigManagerUserConfig

- (字串) CreationClassName

- (字串) Description

- (布林值) DirtyBitSet

- (字串) DriveLetter

- (UInt32) DriveType

- (布林值) ErrorCleared

- (字串) ErrorDescription

- (字串) ErrorMethodology

- (字串) FileSystem

- (UInt64) FreeSpace

- (布林值) IndexingEnabled

- (日期時間) InstallDate

- (字串) Label

- (UInt32) LastErrorCode

- (UInt32) MaximumFileNameLength

- (字串) Name

- (UInt64) NumberOfBlocks

- (字串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布林值) PowerManagementSupported

- (字串) Purpose

- (布林值) QuotasEnabled

- (布林值) QuotasIncomplete

- (布林值) QuotasRebuilding

- (UInt32) SerialNumber

- (字串) Status

- (UInt16) StatusInfo

- (布林值) SupportsDiskQuotas

- (布林值) SupportsFileBasedCompression

- (字串) SystemCreationClassName

- (字串) SystemName



## <a name="ccm_webappinstallinfo"></a>CCM_WebAppInstallInfo

命名空間：root\ccm\cimodels

類別 CCM_WebAppInstallInfo


- (字串) AppDeliveryTypeId

- (UInt32) AppDtRevision

- (字串) TargetURL

- (字串) UserSID

- (字串) URLFileName

- (字串) URLPath



## <a name="sms_windows8application"></a>SMS_Windows8Application

命名空間：root\cimv2\sms

類別 SMS_Windows8Application


- (字串) FullName

- (字串) ApplicationName

- (字串) Architecture

- (布林值) ConfigMgrManaged

- (字串) DependencyApplicationNames

- (字串) FamilyName

- (字串) InstalledLocation

- (布林值) IsFramework

- (字串) Publisher

- (字串) PublisherId

- (字串) Version



## <a name="sms_windows8applicationuserinfo"></a>SMS_Windows8ApplicationUserInfo

命名空間：root\cimv2\sms

類別 SMS_Windows8ApplicationUserInfo


- (字串) FullName

- (字串) UserSecurityId

- (字串) InstallState

- (字串) UserAccountName



## <a name="windows-update"></a>Windows Update

命名空間：root\cimv2

類別 Win32Reg_SMSWindowsUpdate


- (字串) InstanceKey

- (UInt32) AUOptions

- (UInt32) NoAutoUpdate

- (UInt32) UseWUServer



## <a name="windows-update-agent-version"></a>Windows Update 代理程式版本

命名空間：root\cimv2\sms

類別 Win32_WindowsUpdateAgentVersion


- (字串) Version



## <a name="write-filter-state"></a>寫入篩選器狀態

命名空間：root\cimv2\sms

類別 CCM_WriteFilterState


- (布林值) WriteFilterEnabled
