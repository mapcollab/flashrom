sbin_PROGRAMS = flashrom

man_MANS = flashrom.8

# FIXME use "config.h" in the future
DEFS += -DFLASHROM_VERSION=\"@VERSION@\" -DCONFIG_DEFAULT_PROGRAMMER=PROGRAMMER_INTERNAL -DSTANDALONE -DCONFIG_DEFAULT_PROGRAMMER_ARGS=\"\"
DEFS += -DNEED_RAW_ACCESS=1

if HAVE_DMIDECODE
if HAVE_DMIDECODE_EXT
DEFS += -DCONFIG_INTERNAL_DMI=0 -DDMIDECODE_PATH=\"@DMIDECODE@\"
else
DEFS += -DCONFIG_INTERNAL_DMI=1 -DDMIDECODE_PATH=\"\"
endif
endif


if HAVE_INTERNAL
internal_SOURCES = \
	board_enable.c \
	cbtable.c \
	coreboot_tables.h \
	chipset_enable.c \
	internal.c \
	processor_enable.c
if HAVE_X86_ONLY_INTERNAL
internal_x86_only_SOURCES = \
	amd_imc.c \
	dmi.c \
	ich_descriptors.c \
	ich_descriptors.h \
	ichspi.c \
	it85spi.c \
	it87spi.c \
	mcp6x_spi.c \
	sb600spi.c \
	wbsio_spi.c
endif
DEFS += -DCONFIG_INTERNAL=1
endif

if HAVE_SERPROG
serprog_SOURCES = serprog.c serprog.h
DEFS += -DCONFIG_SERPROG=1
endif

if HAVE_LINUX_SPI
linux_spi_SOURCES = linux_spi.c
DEFS += -DCONFIG_LINUX_SPI=1
endif

if HAVE_RAYER_SPI
rayer_spi_SOURCES = rayer_spi.c
DEFS += -DCONFIG_RAYER_SPI=1
endif

if HAVE_PONY_SPI
pony_spi_SOURCES = pony_spi.c
DEFS += -DCONFIG_PONY_SPI=1
endif

if HAVE_BITBANG_SPI
bitbang_spi_SOURCES = bitbang_spi.c
DEFS += -DCONFIG_BITBANG_SPI=1
endif

if HAVE_NIC3COM
nic3com_SOURCES = nic3com.c
DEFS += -DCONFIG_NIC3COM=1
endif

if HAVE_GFXNVIDIA
gfxnvidia_SOURCES = gfxnvidia.c
DEFS += -DCONFIG_GFXNVIDIA=1
endif

if HAVE_SATASII
satasii_SOURCES = satasii.c
DEFS += -DCONFIG_SATASII=1
endif

if HAVE_ATAHPT
atahpt_SOURCES = atahpt.c
DEFS += -DCONFIG_ATAHPT=1
endif

if HAVE_ATAVIA
atavia_SOURCES = atavia.c
DEFS += -DCONFIG_ATAVIA=1
endif

if HAVE_IT8212
it8212_SOURCES = it8212.c
DEFS += -DCONFIG_IT8212=1
endif

if HAVE_FT2232_SPI
ft_2232_spi_SOURCES = ft2232_spi.c
DEFS += -DCONFIG_FT2232_SPI=1
endif

if HAVE_DUMMY
dummy_SOURCES= dummyflasher.c
DEFS += -DCONFIG_DUMMY=1
endif

if HAVE_DRKAISER
drkaiser_SOURCES = drkaiser.c
DEFS += -DCONFIG_DRKAISER=1
endif

if HAVE_NICREALTEK
nicrealtek_SOURCES = nicrealtek.c
DEFS += -DCONFIG_NICREALTEK=1
endif

if HAVE_NICNATSEMI
nicnatsemi_SOURCES = nicnatsemi.c
DEFS += -DCONFIG_NICNATSEMI=1
endif

if HAVE_NICINTEL
nicintel_SOURCES = nicintel.c
DEFS += -DCONFIG_NICINTEL=1
endif

if HAVE_NICINTEL_SPI
nicintel_spi_SOURCES = nicintel_spi.c
DEFS += -DCONFIG_NICINTEL_SPI=1
endif

if HAVE_NICINTEL_EEPROM
nicintel_eeprom_SOURCES = nicintel_eeprom.c
DEFS += -DCONFIG_NICINTEL_EEPROM=1
endif


if HAVE_GFXOGP
gfxogp_SOURCES = ogp_spi.c
DEFS += -DCONFIG_OGP_SPI=1
endif

if HAVE_BUSPIRATE_SPI
buspirate_SOURCES = buspirate_spi.c
DEFS += -DCONFIG_BUSPIRATE_SPI=1
endif

if HAVE_DEDIPROG
dediprog_SOURCES = dediprog.c
DEFS += -DCONFIG_DEDIPROG=1
endif

if HAVE_SATAMV
satamv_SOURCES = satamv.c
DEFS += -DCONFIG_SATAMV=1
endif

if HAVE_SERIAL
serial_SOURCES = serial.c
endif

if HAVE_USBBLASTER_SPI
usbblaster_SOURCES = usbblaster_spi.c
DEFS += -DCONFIG_USBBLASTER_SPI=1
endif

if HAVE_PRINT_WIKI
print_wiki_SOURCES = print_wiki.c
DEFS += -DCONFIG_PRINT_WIKI=1
endif

if HAVE_PCI
pci_SOURCES = pcidev.c \
	      physmap.c \
	      hwaccess.c \
	      hwaccess.h
DEFS += -DNEED_PCI=1
endif

chip_SOURCES = 82802ab.c \
	       at45db.c \
	       chipdrivers.h \
	       flashchips.c \
	       flashchips.h \
	       en29lv640b.c \
	       jedec.c \
	       opaque.c \
	       sfdp.c \
	       spi.c \
	       spi.h \
	       spi25_statusreg.c \
	       spi25.c \
	       sst_fwhub.c \
	       sst28sf040.c \
	       sst49lfxxxc.c \
	       stm50.c \
	       w29ee011.c \
	       w39.c

cli_SOURCES = \
	cli_classic.c \
	cli_common.c \
	cli_output.c \
	print.c

lib_SOURCES = flashrom.c \
	      helpers.c \
	      layout.c \
	      programmer.c \
	      programmer.h \
	      udelay.c

flashrom_SOURCES = \
	flash.h \
	$(internal_SOURCES) \
	$(internal_x86_only_SOURCES) \
	$(serprog_SOURCES) \
	$(linux_spi_SOURCES) \
	$(rayer_spi_SOURCES) \
	$(pony_spi_SOURCES) \
	$(bitbang_spi_SOURCES) \
	$(nic3com_SOURCES) \
	$(gfxnvidia_SOURCES) \
	$(satasii_SOURCES) \
	$(atahpt_SOURCES) \
	$(atavia_SOURCES) \
	$(it8212_SOURCES) \
	$(ft_2232_spi_SOURCES) \
	$(dummy_SOURCES) \
	$(drkaiser_SOURCES) \
	$(nicrealtek_SOURCES) \
	$(nicnatsemi_SOURCES) \
	$(nicintel_SOURCES) \
	$(nicintel_eeprom_SOURCES) \
	$(nicintel_spi_SOURCES) \
	$(gfxogp_SOURCES) \
	$(buspirate_SOURCES) \
	$(dediprog_SOURCES) \
	$(satamv_SOURCES) \
	$(serial_SOURCES) \
	$(usbblaster_SOURCES) \
	$(print_wiki_SOURCES) \
	$(pci_SOURCES) \
	$(chip_SOURCES) \
	$(cli_SOURCES) \
	$(lib_SOURCES)

EXTRA_DIST = COPYING Documentation README util arch.h os.h util flashrom.8.tmpl

BUILT_SOURCES = flashrom.8

flashrom.8: flashrom.8.tmpl
	@sed -e '1 s#".*".*#"$(shell ./util/getrevision.sh -d flashrom.8.tmpl)" "$(VERSION)"#' <$< >$@
