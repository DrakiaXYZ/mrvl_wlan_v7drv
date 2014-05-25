ifeq (24,$(BUILD))
USE_STANDARD_AS_RULE := true
O_TARGET := ap85.o
obj-y		:=
obj-m		:=
obj-n		:=
obj-		:=
DRIVER-OBJS = driver-objs
API-OBJS = api-objs
AP-OBJS = ap-objs
else
DRIVER-OBJS = ap8x-objs
API-OBJS = ap8x-objs
AP-OBJS = ap8x-objs
endif

ifeq (W8363, $(SOC))
	#Compile 8 BSS by default; assuming all cards are SF3-A5 or beyond
	APS=8
else
	#default SOC to W8366 B0
	ifeq (W8366A1, $(SOC))
		APS=1
	else
		APS=8
	endif
endif
#Set equal to 1 to build with client code, else 0
BUILD_CLIENT=1

#Cap Tx max rate
BUILD_CAP_MAX_RATE=1

ifeq (1, $(BUILD_CLIENT))
#Set equal to 1 in order compile in WPS client code
BUILD_WPS_CLIENT=1
#Set equal to 1 in order to compile DFS channel support and DFS passive scan for channels 52 to 64 and 100 to 140
BUILD_DFS_PASSIVE_SCAN = 1
#Set equal to 1 to include EWB FEATURE
BUILD_EWB=1
endif

#Set equal to 1 in order compile in multicast proxy code
BUILD_MPRXY=1
#Set equal to 1 to include TSO SUPPORT
#Enable TSO by default for L26; L24 does not support TSO
ifeq (24,$(BUILD))
BUILD_TSO=0
else
BUILD_TSO=1
endif
#Set equal to 1 to include Dynamic BA Support
BUILD_DYNAMIC_BA=1
#Set equal to 1 to include WFA 11n TKIP Negative tests
BUILD_WFA_TKIP_NEGATIVE = 1

#set equal to 1 to include rx path interrupt reduction
BUILD_RXPATHOPT=0

#set to 1 to enable tcp ack enhancement
BUILD_TCP_ACK_ENHANCEMENT = 1

#Set equal to 1 to include SC2 Palladium simulation development.
PALLADIUM=0

#Set equal to 1 to include spectrum support.
BUILD_SSU_SUPPORT = 0

ifeq (1, $(PALLADIUM))
BUILD_SC_PALLADIUM=1
endif

#Set equal to 1 to enable packet statistics code.
BUILD_QUEUE_STATS_LATENCY=0
BUILD_QUEUE_STATS_CNT_HIST=1

#Set equal to 1,2, or 3 to enable packet statistics code in compile time.
ifeq (1, $(QUEUE_STATS))
BUILD_QUEUE_STATS_LATENCY=1
endif
ifeq (2, $(QUEUE_STATS))
BUILD_QUEUE_STATS_CNT_HIST=1
endif
ifeq (3, $(QUEUE_STATS))
BUILD_QUEUE_STATS_LATENCY=1
BUILD_QUEUE_STATS_CNT_HIST=1
endif

$(DRIVER-OBJS)	:= \
		driver/linux/ap8xLnxDesc.o 	\
		driver/linux/ap8xLnxFwdl.o		\
		driver/linux/ap8xLnxFwcmd.o		\
		driver/linux/ap8xLnxIntf.o		\
		driver/linux/ap8xLnxApi.o		\
		driver/linux/ap8xLnxRecv.o		\
		driver/linux/ap8xLnxXmit.o		\
		driver/linux/ap8xLnxStat.o		\
		driver/linux/ap8xLnxWlLog.o	\
		driver/linux/ap8xLnxDump.o


$(API-OBJS)	+= \
		core/api/wlFun.o		\
		core/api/wlApi.o

$(AP-OBJS)		+= \
		core/dbg/wldebug.o 		\
		core/encr/aes_key_wrap.o \
		core/encr/hmac_md5.o \
		core/encr/prfapi.o \
		core/encr/pbkdf2.o \
		core/encr/md5.o \
		core/encr/sha1.o \
		core/encr/tkip.o \
		core/encr/AP/ccmpAP.o \
		core/encr/AP/keyMgmt.o \
		core/encr/AP/tkipAP.o \
		core/wlsys/bcngen.o \
		core/wlsys/hal_mib.o \
		core/wlsys/hal_sys.o \
		core/wlsys/w81init.o \
		core/mgt/mhsm.o \
		core/mgt/List.o \
		core/mgt/timer.o \
		core/mgt/AP/AssocSrvAp.o \
		core/mgt/AP/AuthSrvAp.o \
		core/mgt/AP/idList.o \
		core/mgt/AP/macmgmtap.o \
		core/mgt/AP/macMgmtEvt.o \
		core/mgt/AP/macMgmtMlme.o \
		core/mgt/AP/mlmeApi.o \
		core/mgt/AP/mlmeAuth.o \
		core/mgt/AP/smeMain.o \
		core/mgt/AP/StaDb.o \
		core/mgt/AP/SyncSrvAp.o \
		core/mgt/AP/util.o \
		core/mgt/AP/wlMlmeSrv.o \
		core/mib/mib.o \
		core/mib/wl_mib.o \
		core/os/os_if.o \
		core/qos/qos.o \
		core/qos/qos_back.o \
		core/qos/AP/qos_dlp.o \
		core/qos/AP/qos_scheduler.o \
		core/wlsys/domain.o \
		core/wlsys/packet.o \
		core/wlsys/fragment.o \
		core/wlsys/autochannel.o \
        core/mgt/AP/dfsSM.o \
        core/mgt/AP/dfsEv.o \
        core/wds/wds.o

ifeq (1, $(BUILD_CLIENT))
	$(AP-OBJS)	+= \
		core/mgt/STA/AssocSta_sm.o \
		core/mgt/STA/AssocSta_srv.o \
		core/mgt/STA/AuthSta_sm.o \
		core/mgt/STA/AuthSta_srv.o \
		core/mgt/STA/SyncSta_sm.o \
		core/mgt/STA/SyncSta_srv.o \
		core/mgt/STA/macMgmtEvtSta.o \
		core/mgt/STA/smeStateMgrSta.o \
		core/mgt/STA/mlmeApiSta.o \
		core/mgt/STA/wlvmac.o \
		core/mgt/STA/child_srv.o \
		core/mgt/STA/parent_srv.o \
		core/mgt/STA/wlMlmeSrvSta.o \
		core/wlsys/linkmgt.o \
		core/wlsys/ewb_hash.o \
		core/wlsys/ewb_packet.o \
		core/encr/STA/keyMgmtSta.o
endif


#obj-$(CONFIG_MARVELL_SOFTAP) += ap8x.o
obj-m += ap8x.o
	
ifeq (24,$(BUILD))
ap8x.o: $(driver-objs) $(api-objs) $(ap-objs) $(sta-objs)
	$(LD) -r -o $@ $(driver-objs) $(api-objs) $(ap-objs) $(sta-objs)

CROSS_COMPILE 	= /opt/toolchain-glibc-3.4.4/bin/arm-linux-gnu-
KDIR:= /home/public/SDK/Linux_kernel/release/linux-gw-ap-2_4-1_1_3
PWD:=$(shell pwd)
else	
CROSS_COMPILE 	= /opt/SDK-5.0/armv7-marvell-linux-gnueabi-softfp/bin/arm-marvell-linux-gnueabi-
KDIR:=/home/public/SDK/ap8x/EEBU_AP9X_SC_DEV/kernel/RD-A370/linux-3.0.6-armada370-3.1.0
PWD:=/home/public/SDK/ap8x/EEBU_AP_11AC_DEV/wlan-v7
#CROSS_COMPILE   = /opt/armel21-26/bin/arm-none-linux-gnueabi-
#KDIR:=/home/ap8x/SDK/LSP_2.6.29/kernel.git
#PWD:=/home/ap8x/wireless_src/AP9X_SC_DEV_VM_01/EEBU_AP_11AC_DEV/wlan-v7
endif

AS		= $(CROSS_COMPILE)as
LD		= $(CROSS_COMPILE)ld
CC		= $(CROSS_COMPILE)gcc

SOC:=$(KDIR)/arch/arm/mach-mv88fxx81

EXTRA_CFLAGS+= -I${KDIR}
ifeq (24,$(BUILD))
EXTRA_CFLAGS+= -DWL_KERNEL_24
else
EXTRA_CFLAGS+= -DWL_KERNEL_26
EXTRA_CFLAGS+= -DUSE_TASKLET
#EXTRA_CFLAGS+= -DNAPI
EXTRA_CFLAGS+= -O2 -funroll-loops
endif

EXTRA_CFLAGS+=-I${PWD} -I${PWD} -I${PWD}/driver/linux -I${PWD}/core/api -I${PWD}/core/incl -I${PWD}/core/mgt/STA/incl
EXTRA_CFLAGS+=-I${SOC} -I${SOC}/Common -I${SOC}/Soc/idma -I${SOC}/Soc/ctrlEnv -I${SOC}/mv88f5181 -I${SOC}/osServices -I${SOC}/osServices/linux/ArchARM
EXTRA_CFLAGS+=-I${SOC}/Board/boardEnv -I${SOC}/Board/boardEnv/DB_88FXX81 -I${SOC}/Soc/ctrlEnv/MV_88FXX81 -I${SOC}/osServices/linux

ifeq (BE,$(ENDIAN))
EXTRA_CFLAGS+=-DMV_CPU_BE
else
EXTRA_CFLAGS+=-DMV_CPU_LE
endif

EXTRA_CFLAGS+=-DMV_LINUX -DMV_ARM

EXTRA_CFLAGS+= -DUDP_API -DAP_MAC_LINUX \
		-DIEEE80211H -DWPA -DAP_WPA2 -DQOS_FEATURE -DSTA_INFO_DB \
		-DBT_COEXISTENCE -DAVOID_MIS_ACC -DQOS_WSM_FEATURE
EXTRA_CFLAGS+= -DEXPORT_SYMTAB
EXTRA_CFLAGS+= -DRELEASE_11N
EXTRA_CFLAGS+= -DAGG_QUE -DAP8X_STATISTICS
EXTRA_CFLAGS+= -DENABLE_WLSNDEVT
EXTRA_CFLAGS+= -DAP8X_DUMP -DAUTOCHANNEL -DENABLE_WLSYSLOG -DUAPSD_SUPPORT
EXTRA_CFLAGS+= -DAMPDU_SUPPORT 
EXTRA_CFLAGS+= -DMRV_8021X 
EXTRA_CFLAGS+= -DINTEROP -DAMSDU_BYTE_REORDER -DIEEE_HTIE
EXTRA_CFLAGS+= -DWDS_FEATURE
EXTRA_CFLAGS+= -DBRS_SUPPORT
EXTRA_CFLAGS+= -DIEEE80211_DH
#EXTRA_CFLAGS+= -DZERO_COPY
EXTRA_CFLAGS+= -DZERO_COPY_RX
EXTRA_CFLAGS+= -DMFG_SUPPORT
EXTRA_CFLAGS+= -DPWRFRAC
EXTRA_CFLAGS+= -DMRVL_WSC
#EXTRA_CFLAGS+= -DMRVL_WAPI
EXTRA_CFLAGS+= -DMRVL_DFS
#EXTRA_CFLAGS+= -DWMON
#EXTRA_CFLAGS+= -DINTOLERANT40
EXTRA_CFLAGS+= -DIEEE80211N_MIMOPSD110
EXTRA_CFLAGS+= -DCOEXIST_20_40_SUPPORT
EXTRA_CFLAGS+= -DGENERIC_GETIE

EXTRA_CFLAGS+= -DWNC_LED_CTRL
ifeq (16, $(APS))
EXTRA_CFLAGS+= -DMCAST_PS_OFFLOAD_SUPPORT
endif

ifeq (1, $(BUILD_RXPATHOPT))
EXTRA_CFLAGS+= -DRXPATHOPT
endif

EXTRA_CFLAGS+= -DMRVL_WPS2
EXTRA_CFLAGS+= -DEXPLICIT_BF
ifeq (1,$(BUILD_TCP_ACK_ENHANCEMENT))
    EXTRA_CFLAGS += -DTCP_ACK_ENHANCEMENT
endif

ifeq (1, $(BUILD_EWB))
EXTRA_CFLAGS+= -DEWB
endif

ifeq (1, $(BUILD_TSO))
EXTRA_CFLAGS+= -DWLAN_INCLUDE_TSO
endif

EXTRA_CFLAGS+= -DMBSS -DCOMMON_PHYDSSS -DMIMO_PS_HT -DNPROTECTION

ifeq (1, $(BUILD_CLIENT))
EXTRA_CFLAGS+= -DCLIENT_SUPPORT -DWPA_STA -DWPA2 -DRSN_RESOLVE -DAMPDU_SUPPORT_TX_CLIENT
endif


ifeq (AP82S,$(PLATFORM))
EXTRA_CFLAGS+= -DAP82S
endif

ifeq (W8363, $(SOC))
EXTRA_CFLAGS+= -DSOC_W8363
else
ifeq (W8364, $(SOC))
EXTRA_CFLAGS+= -DSOC_W8364
else
ifeq (W8864, $(SOC))
EXTRA_CFLAGS+= -DSOC_W8764 -DSOC_W8864
else
EXTRA_CFLAGS+= -DSOC_W8366
endif
endif
endif

ifeq (1, $(WLDBG))
EXTRA_CFLAGS+= -DWL_DEBUG
endif

ifeq (1, $(NOFWDL))
EXTRA_CFLAGS+= -DNO_FW_DOWNLOAD
endif

ifeq (1, $(MFGFW))
EXTRA_CFLAGS+= -DDEFAULT_MFG_MODE
endif

ifneq (1, $(WLMEM))
EXTRA_CFLAGS+= -DWLMEM_DISABLED
endif

ifeq (1, $(BUILD_MPRXY))
EXTRA_CFLAGS+= -DMPRXY -DMPRXY_SNOOP -DMPRXY_IGMP_QUERY
endif

ifeq (1, $(BULID_CLIENT_ONLY))
EXTRA_CFLAGS+= -DCLIENTONLY -DSINGLE_DEV_INTERFACE
endif

ifeq (, $(APS))
EXTRA_CFLAGS+= -DNUMOFAPS=1
else
EXTRA_CFLAGS+= -DNUMOFAPS=$(APS)
endif

ifeq (1, $(V4FW))
EXTRA_CFLAGS+= -DAMPDU_SUPPORT_SBA
EXTRA_CFLAGS+= -DV4FW
endif

ifeq (1, $(BUILD_WPS_CLIENT))
EXTRA_CFLAGS+= -DMRVL_WPS_CLIENT
endif
ifeq (1, $(BUILD_DFS_PASSIVE_SCAN))
EXTRA_CFLAGS+= -DDFS_PASSIVE_SCAN -DDFS_CHNL_SUPPORT -DFCC_15E_INTERIM_PLAN
endif
EXTRA_CFLAGS+= -DBA_WATCHDOG
EXTRA_CFLAGS+= -DV6FW -DATTN_RSSI -DAMPDU_SUPPORT_SBA
ifeq (1, $(BUILD_DYNAMIC_BA))
EXTRA_CFLAGS+= -DDYNAMIC_BA_SUPPORT
endif
EXTRA_CFLAGS+= -DAMSDUOVERAMPDU
ifeq (1, $(BUILD_WFA_TKIP_NEGATIVE))
EXTRA_CFLAGS+= -DWFA_TKIP_NEGATIVE
endif
ifeq (1, $(BUILD_SC_PALLADIUM))
EXTRA_CFLAGS+= -DSC_PALLADIUM
endif
ifeq (1, $(BUILD_SSU_SUPPORT))
EXTRA_CFLAGS+= -DSSU_SUPPORT
endif
ifeq (1, $(BUILD_QUEUE_STATS_LATENCY))
EXTRA_CFLAGS+= -DQUEUE_STATS_LATENCY -DQUEUE_STATS
endif
ifeq (1, $(BUILD_QUEUE_STATS_CNT_HIST))
EXTRA_CFLAGS+= -DQUEUE_STATS_CNT_HIST
ifeq (0, $(BUILD_QUEUE_STATS_LATENCY))
EXTRA_CFLAGS+= -DQUEUE_STATS
endif
endif
ifeq (1, $(BUILD_CAP_MAX_RATE))
EXTRA_CFLAGS+= -DCAP_MAX_RATE
endif

#include $(TOPDIR)/Rules.make
ifeq (24,$(BUILD))
include $(KDIR)/Rules.make
endif
all:
	@echo $(if $(findstring MRVL_WPS2,$(EXTRA_CFLAGS)),MRVL_WPS2 defined,Info: MRVL_WPS2 not defined)
	$(MAKE) -C $(KDIR) SUBDIRS=$(PWD) modules

ifeq (24,$(BUILD))
clean:
	rm -f *.o $(driver-objs) $(api-objs) $(ap-objs) $(sta-objs)
else
clean:
	rm -f *.o *.a *.s *.ko *.ko.cmd *.o.cmd *.mod.* .ap8x.* $(ap8x-objs)
	find . -name .*.o.cmd -exec rm -f {} \;
endif
