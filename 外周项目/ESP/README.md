ESP模块可操作EFI分区，为C++和C#开发者提供一个仅基于原生WindowsAPI而不是基于进程的模块。

# 功能支持

|功能|C++|C#(CLR版本)| 
|---|---|---|
|挂载EFI分区|&#10003;|&#10003;| 
|卸载EFI分区|&#10003;|&#10003;| 
|获取EFI分区参数|&#10003;|&#10005; | 

# ESP参考

## 公开函数

### Esp_MountEfiPartition（重载1）

```CPP
BOOL Esp_MountEfiPartition(_Out_ std::vector<char>* MountedEspLetter);
```

#### 功能
挂载所有EFI分区，已挂载的分区不会重复挂载

#### 参数

##### [Out] MountedEspLetter
指向用于接收存储挂载的EFI分区盘符的vector容器的指针

#### 返回
挂载成功返回1，同时**MountedEspLetter**中会存放挂载的EFI分区盘符。 \
如果没有EFI分区被挂载，函数返回0，GetLastError()=ERROR_GETESPINFO_NO_ESP_PARTITION  \
挂载失败返回0，可用[GetLastError()](https://learn.microsoft.com/zh-CN/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror)获取详细错误参数。

### Esp_MountEfiPartition（重载2）
```CPP
BOOL Esp_MountEfiPartition(_In_ int DiskNumber, _Out_ std::vector<char>* MountedEspLetter);
```

#### 功能
挂载指定硬盘编号的EFI分区，已挂载的不会重新挂载

#### 参数

##### [In] DiskNumber
欲执行EFI分区挂载操作的硬盘的编号，从0开始

##### [Out] MountedEspLetter
指向用于接收存储挂载的EFI分区盘符的vector容器的指针

#### 返回
挂载成功返回1，同时**MountedEspLetter**中会存放挂载的EFI分区盘符。 \
如果没有EFI分区被挂载，函数返回0，GetLastError()=ERROR_GETESPINFO_NO_ESP_PARTITION  \
挂载失败返回0，可用[GetLastError()](https://learn.microsoft.com/zh-CN/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror)获取详细错误参数。 

### Esp_UnmountEfiPartition（重载1）

```CPP
BOOL Esp_UnmountEfiPartition(_Out_ std::vector<char>* UnmountedEspLetter);
```

#### 功能
卸载所有EFI分区，已卸载的分区不会重复挂载

#### 参数

##### [Out] UnmountedEspLetter
指向用于接收存储已卸载的EFI分区盘符的vector容器的指针

#### 返回
卸载成功返回1，同时**UnmountedEspLetter**中会存放已卸载的EFI分区盘符。 \
如果没有EFI分区被卸载，函数同样会返回1，同时**UnmountedEspLetter**为空。 \
卸载失败返回0，可用[GetLastError()](https://learn.microsoft.com/zh-CN/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror)获取详细错误参数。 

### Esp_UnmountEfiPartition（重载2）

```CPP
BOOL Esp_UnmountEfiPartition(_In_ char Letter);
```

#### 功能
卸载指定的EFI分区。

#### 参数

##### [In] Letter
欲卸载的EFI分区所对应的盘符

#### 返回
卸载成功返回1， \
卸载失败返回0，可用[GetLastError()](https://learn.microsoft.com/zh-CN/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror)获取详细错误参数。 

### Esp_UnmountEfiPartition（重载3）
```CPP
BOOL Esp_UnmountEfiPartition(_In_ int DiskNumber, _Out_ std::vector<char>* UnmountedEspLetter);
```

#### 功能
卸载所有EFI分区，已卸载的分区不会重复挂载

#### 参数

##### [In] DiskNumber
欲执行EFI分区卸载操作的硬盘的编号，从0开始

##### [Out] UnmountedEspLetter
指向用于接收存储已卸载的EFI分区盘符的vector容器的指针

#### 返回
卸载成功返回1，同时**UnmountedEspLetter**中会存放已卸载的EFI分区盘符。 \
如果没有EFI分区被卸载，函数同样会返回1，同时**UnmountedEspLetter**为空。 \
卸载失败返回0，可用[GetLastError()](https://learn.microsoft.com/zh-CN/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror)获取详细错误参数。

### Efi_GetEfiPartitionInfoTableA
```CPP
BOOL Efi_GetEfiPartitionInfoTableA(
	_Out_ std::vector<EFI_PARTITION_INFOMATION_A*>* PartitionInfo
);
```
#### 功能
获取计算机上所有EFI分区信息(char型)

#### 参数
##### [Out] PartitionInfo
指向存放EFI_PARTITION_INFOMATION_A结构体指针的vector容器的指针

#### 返回
获取成功返回1，同时**PartitionInfo**会存放EFI_PARTITION_INFOMATION_A结构体指针 \
获取失败返回0，可用[GetLastError()](https://learn.microsoft.com/zh-CN/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror)获取详细错误参数。

### Efi_GetEfiPartitionInfoTableW
```CPP
BOOL Efi_GetEfiPartitionInfoTableW(
	_Out_ std::vector<EFI_PARTITION_INFOMATION_W*>* PartitionInfo
);
```
#### 功能
获取计算机上所有EFI分区信息(w_char型)

#### 参数
##### [Out] PartitionInfo
指向存放EFI_PARTITION_INFOMATION_W结构体指针的vector容器的指针

#### 返回
获取成功返回1，同时**PartitionInfo**会存放EFI_PARTITION_INFOMATION_W结构体指针 \
获取失败返回0，可用[GetLastError()](https://learn.microsoft.com/zh-CN/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror)获取详细错误参数。


## 公开结构体

### EFI_PARTITION_INFOMATION_A

```CPP
typedef struct EFI_PARTITION_INFOMATION_A {
	int DiskNumber;					

	std::string PartionDrivePathA;	

	bool HasPartitionLetter;		
	char PartitionLetter;			
};
```
#### DiskNumber
EFI分区所在硬盘编号，从0开始

#### PartionDrivePathA
分区路径，如"\\Device\\Harddisk0\\Partition1"，可通过该路径挂载和卸载EFI分区

#### HasPartitionLetter
分区是否被挂载，true为挂载，false为未挂载

#### PartitionLetter
若**HasPartitionLetter**为true，则**PartitionLetter**为该EFI分区挂载的盘符;
若**HasPartitionLetter**为false，则**PartitionLetter**为NULL。

### EFI_PARTITION_INFOMATION_W
```CPP
typedef struct EFI_PARTITION_INFOMATION_W {
	int DiskNumber;					
	
	std::wstring PartionDrivePathW;	

	bool HasPartitionLetter;		
	char PartitionLetter;			
};
```
#### DiskNumber
EFI分区所在硬盘编号，从0开始

#### PartionDrivePathW
分区路径，如"\\Device\\Harddisk0\\Partition1"，可通过该路径挂载和卸载EFI分区

#### HasPartitionLetter
分区是否被挂载，true为挂载，false为未挂载

#### PartitionLetter
若**HasPartitionLetter**为true，则**PartitionLetter**为该EFI分区挂载的盘符;
若**HasPartitionLetter**为false，则**PartitionLetter**为NULL。

## 函数别称
```CPP
#define Efi_GetEfiPartitionInfoTable Efi_GetEfiPartitionInfoTableW
#define Esp_GetEfiPartitionInfoTable Efi_GetEfiPartitionInfoTableW
#define Esp_GetEfiPartitionInfoTableW Efi_GetEfiPartitionInfoTableW
#define Esp_GetEfiPartitionInfoTableA Efi_GetEfiPartitionInfoTableA
```

|原函数名|可用别称|
|-|-|
|Efi_GetEfiPartitionInfoTableW|Efi_GetEfiPartitionInfoTable|
|Efi_GetEfiPartitionInfoTableW|Esp_GetEfiPartitionInfoTable|
|Efi_GetEfiPartitionInfoTableW|Esp_GetEfiPartitionInfoTableW|
|Efi_GetEfiPartitionInfoTableA|Esp_GetEfiPartitionInfoTableA|

## 公开错误代码
### ERROR_GETDRVINFO_NODISK(1)
计算机中没有磁盘

### ERROR_GETDRVINFO_OPEN_DISK_FAIL(2)
通过CreateFile打开磁盘失败

### ERROR_GETDRVINFO_GET_STRUCT_SIZE_FAIL(3)
获取结构体大小失败

### ERROR_GETDRVINFO_GET_STRUCT_FAIL(4)
获取结构体失败

### ERROR_GETVOLUME_GET_VOLUME_MOUNT_PATH_FAIL(5)
获取卷挂载路径失败

### ERROR_GETESPINFO_NO_ESP_PARTITION(6)
没有ESP分区

### ERROR_GETESPINFO_NO_MORE_AVAIBLE_LETTER(7)
没有多余盘符(获取可用盘符)

### ERROR_MOUNTESP_NO_MORE_AVAIBLE_LETTER(8)
没有多余盘符(挂载ESP)

