TESTBENCH   = tb.sv

# HEADERS     = $(OPENTITAN_PKGS)/prim/rtl/prim_pkg.sv
# HEADERS    += $(OPENTITAN_PKGS)/prim/rtl/prim_util_pkg.sv
# HEADERS    += $(OPENTITAN_TOP)/top_pkg.sv
# HEADERS    += $(OPENTITAN_IBEX)/rtl/ibex_pkg.sv
# HEADERS    += $(OPENTITAN_IBEX)/vendor/lowrisc_ip/ip/prim/rtl/prim_ram_1p_pkg.sv
# HEADERS    += $(OPENTITAN_PKGS)/uart/rtl/uart_reg_pkg.sv
# HEADERS    += $(OPENTITAN_PKGS)/tlul/rtl/tlul_pkg.sv
# HEADERS    += $(OPENTITAN_PKGS)/xbar/xbar_pkg.sv
# HEADERS    += $(OPENTITAN_PKGS)/rv_plic/rtl/rv_plic_reg_pkg.sv
# HEADERS    += $(OPENTITAN_PKGS)/gpio/rtl/gpio_reg_pkg.sv
HEADERS		= $(wildcard ../common/*.sv)
SIMFILES    = $(wildcard src/*.sv ../xbar_periph/src/*.sv)

VCS = SW_VCS=2017.12-SP2-1 vcs -sverilog -debug_pp\
	+vc +v2k -Mupdate -line -full64  -timescale=1ps/1fs\
	+notimingcheck +memcbk +vcs+dumparrays +sdfverbose\
	+define+DUMP_VCD=1 +define+ARM_UD_MODEL 

all:    simv
	./simv | tee program.out

sim:	simv
	./simv | tee program.out

simv:  $(HEADERS) $(SIMFILES) $(TESTBENCH)
	$(VCS) $^ -o simv

dve:	sim
	./simv -gui &

clean:
	@rm -rf *simv *simv.daidir csrc vcs.key *.key
	@rm -rf vis_simv vis_simv.daidir
	@rm -rf dve* inter.vpd DVEfiles
	@rm -rf csrc vcdplus.vpd vc_hdrs.h
	@rm -f *.out *.elf *.dump *.mem *.log
	@rm -f debug_bin
	@rm -f .__*
	@rm -f default.svf
	@rm -rf simv.vdb
	@rm -rf urgReport
	@rm -rf .restartSimSession.tcl.old .synopsys_dve_rebuild.tcl

nuke:   clean
