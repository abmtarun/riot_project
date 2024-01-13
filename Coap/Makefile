#Makefile for Coap
APPLICATION = Coap

BOARD ?= iotlab-m3

RIOTBASE ?= $(CURDIR)/../../RIOT

GCOAP_RESEND_BUFS_MAX ?= 2
CFLAGS += -DCONFIG_GCOAP_RESEND_BUFS_MAX=$(GCOAP_RESEND_BUFS_MAX)

USEMODULE += netdev_default
USEMODULE += auto_init_gnrc_netif

USEMODULE += gnrc_ipv6_default
USEMODULE += gcoap

USEMODULE += gnrc_icmpv6_echo


USEMODULE += od
USEMODULE += fmt

USEMODULE += shell
USEMODULE += shell_commands
USEMODULE += ps


USEMODULE += lps331ap


DEVELHELP ?= 1


QUIET ?= 1

include $(RIOTBASE)/Makefile.include


include $(RIOTMAKE)/default-radio-settings.inc.mk


ifndef CONFIG_KCONFIG_MODULE_GCOAP

GCOAP_RESEND_BUFS_MAX ?= 2
CFLAGS += -DCONFIG_GCOAP_RESEND_BUFS_MAX=$(GCOAP_RESEND_BUFS_MAX)
endif

