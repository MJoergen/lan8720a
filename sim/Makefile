XILINX_DIR = /opt/Xilinx/Vivado/2019.2

SRC_DIR = ../src
SRC  = $(SRC_DIR)/rmii_rx.vhd
SRC += $(SRC_DIR)/rmii_tx.vhd
SRC += $(SRC_DIR)/lan8720a.vhd

TB = lan8720a_tb
TB_SRC  = sim_tx.vhd
TB_SRC += sim_rx.vhd
TB_SRC += $(TB).vhd

WAVE = build/$(TB).ghw
SAVE = $(TB).gtkw


#####################################
# Simulation
#####################################

show: $(WAVE) $(SAVE)
	gtkwave $(WAVE) $(SAVE)

$(WAVE): $(SRC) $(TB_SRC) build
	ghdl -i --std=08 --work=unisim $(XILINX_DIR)/data/vhdl/src/unisims/unisim_VCOMP.vhd
	ghdl -i --std=08 --work=unisim $(XILINX_DIR)/data/vhdl/src/unisims/unisim_VPKG.vhd
	ghdl -i --std=08 --work=unisim $(XILINX_DIR)/data/vhdl/src/unisims/primitive/*.vhd
	ghdl -i --std=08 --work=work $(SRC) $(TB_SRC)
	ghdl -m --std=08 -frelaxed-rules $(TB)
	ghdl -r $(TB) --assert-level=error --wave=$(WAVE) --stop-time=1us

build:
	mkdir -p build


#####################################
# Cleanup
#####################################

clean:
	rm -rf build
	rm -rf *.o
	rm -rf $(TB)
	rm -rf unisim-obj08.cf
	rm -rf work-obj08.cf

