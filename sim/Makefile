fifo_run_test: clean
        qverilog -vopt +acc ../rtl/uart_fifo.v ../tb/uart_fifo_tb.v
        vsim work.tb -voptargs=+acc

tx_run_test: clean
        qverilog -vopt +acc ../rtl/uart_fifo.v ../rtl/tx.v ../tb/tx_tb.v
        vsim work.uart_tx_tb -voptargs=+acc

rx_run_test: clean
        qverilog -vopt +acc ../rtl/uart_fifo.v ../rtl/rx.v ../tb/rx_tb.v
        vsim work.uart_rx_tb -voptargs=+acc

uart_16550_run_test: clean
        qverilog -vopt +acc ../rtl/uart_fifo.v ../rtl/tx.v ../rtl/rx.v ../rtl/uart_register_file.v ../rtl/uart_16550.v ../tb/uart_16550_tb.v
        vsim work.uart_16550_tb -voptargs=+acc

cmp: clean
        vcs -full64 -sverilog -debug_access+all -P $(FSDB_PATH)/novas.tab $(FSDB_PATH)/pli.a ../rtl/uart_fifo.v ../rtl/tx.v ../rtl/rx.v ../rtl/uart_register_file.v ../rtl/uart_16550.v ../tb/uart_16550_tb.v -l vcs_compile.log

vcs_uart_16550_run_test: cmp
        ./simv +fsdbfile+wave.fsdb -l vcs_sim.log

clean:
        rm -rf simv simv.daidir csrc ucli.key dump.fsdb wave.fsdb wave.vcd qverilog.log work vsim.wlf transcript verdiLog dump.vcd novas.conf novas.rc
        clear

#view_wave:
#       vsim work.tb -voptargs=+acc
