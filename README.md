# AzureIaaSVMWin2016FileShare2016FCI

안녕하세요…

지난 포스팅 이후로 한달여 만에 인사드립니다.
이번 포스팅은 아래 지난 포스팅에 이은 Azure IaaS VM으로 Failover Clustering을 구축하는 다른 방법을 소개합니다. 아래 포스팅은 Azure IaaS VM 상에서 Failover Clustering을 구성할 때, “Azure Shared Disk” 를 사용한 방법을 소개했습니다. 또한, 아래 포스팅에서는 Failover Clustering을 구현 한 후, 실제 SQL Server의 High Availability 를 구현했습니다.

AzureIaaSVMWin2016SQL2016FCI (https://github.com/dongclee/AzureIaaSVMWin2016SQL2016FCI)

본 포스팅에서는, Azure IaaS VM 상에서 Failover Clustering을 구성할 때, “Windows Server 2016 Datacenter 버전 저장소 공간 다이렉트 (S2D) (https://learn.microsoft.com/ko-kr/azure-stack/hci/concepts/storage-spaces-direct-overview)”를 사용한 방법을 소개합니다. 또한, 이렇게 구성한 Failover Clustering 상에서, “파일 공유 서비스” 에 대한 High Availability 를 구현하는 방법을 소개합니다.

기본적인, S2D 에 대한 개념 소개는 아래와 같습니다. S2D는 Windows Server 2016 버전 이상에서 지원이 가능합니다. 다음 다이어그램에서는 Azure 가상 머신에서 구현한 S2D의 기본적인 구성도입니다.

<img width="258" alt="image" src="https://user-images.githubusercontent.com/42400574/227258889-151d5cd3-9125-415f-bb67-421b7ba49ee6.png">

위의 다이어그램은 다음을 보여 줍니다.

● Windows 장애 조치(Failover) 클러스터에 있는 두 개의 Azure Virtual Machines 가상 머신이 장애 조치 클러스터에 있는 경우 클러스터 노드 또는 노드라고도 합니다.

● 각 가상 머신에는 두 개 이상의 데이터 디스크가 있습니다.

● S2D는 데이터 디스크의 데이터를 동기화하고 저장소 풀로 동기화된 저장소를 제공합니다.

● 저장소 풀은 장애 조치 클러스터에 CSV(클러스터 공유 볼륨)를 제공합니다.

● File Server FCI(Failover Clustering Instance) 클러스터 역할은 데이터 드라이브에 CSV를 사용하지 않습니다. 만약, SQL Server FCI (Failover Clustering Instance) 클러스터 역할을 구성한다면 데이터 드라이브에 CSV를 사용해야 합니다.

● File Server FCI에 대한 IP 주소를 저장하는 Azure 부하 분산 장치.

● Azure 가용성 집합은 모든 리소스를 보유합니다.

(참고) 다이어그램의 모든 Azure 리소스는 동일한 리소스 그룹에 있습니다.

제가 만든 Step by Step 가이드에서 구성 환경은 아래와 같습니다.

<img width="456" alt="image" src="https://user-images.githubusercontent.com/42400574/227259138-68bd40eb-8c41-45cf-a949-58dfde8c73c8.png">

또한, 위 구성 환경으로 구성한 데모 환경은 아래와 같습니다.

<img width="453" alt="image" src="https://user-images.githubusercontent.com/42400574/227259317-94c4f789-e9b8-48a2-a9e8-bca080b3241e.png">

본 데모 환경에서는 “파일 공유 서비스” 에 대한 High Availability 를 구현했지만, 본 문서의 4단계 부분을 “SQL Server” 의 AlwaysOn 또는 FCI 로 대체하면, SQL Server 에 대한 High Availability 를 구현할 수 있습니다. 

이렇게 오늘자 포스팅은 마무리하도록 하겠습니다.

감사합니다.

[Azure Virtual Machines에 File Server 장애 조치.pdf](https://github.com/dongclee/AzureIaaSVMWin2016FileShare2016FCI/files/11052983/Azure.Virtual.Machines.File.Server.pdf)
