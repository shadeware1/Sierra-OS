s_
 
[3.5] | { 
       //This file is in charge of booting Sierra 11 and loading the modified kernel via disk
       //written by AP-77
}

[3.5] | {
       $use_bios.pkg 
       read.terminal(ivf) page 
       disk_read (system_disk) read pkg('s') 
       [terminal.sdl; diskread.sdl;]
}

[1.5] | {
       fn main_boot(v:__00) 
       terminal.dis bin:txt dis.txt = ("Sierra 11 Bootloader") gCD:_disk(display-head) 
       terminal.dis bin:txt dis.txt = ("Init CPU...") 
       cpu.enter_protectMode mem.init {
            load.kernel(sys_kernel(%disk%)) {
                    cpu.cmd(^cpu_jumper) jump fn { 
                            jump.kernel cpuJump_kernel*dst  
                    }
            }

       }
}

[3.5] | {
       space cpu(parse_meter) {
            fpl enter_protecMode 
            bios.cmd(^bios_cmd_exec) load_gdt bios.enable protectMode = true 
            sub.parse(fnp_func) {
                    exec_v {
                            kernel_jump(empty) value:repo 
                            bios.jump(^//cmd) = 0x100000
                    }
            }
       }
}

[3.5] | {
       set.reg for boot 
       space(mem) {
            fnl init(empty) {
                    skip.mem implemented
            }
       }
}

[3.5] | {
       space kernel {
            fn load(boot) 
            let path = "A:\\boot\\kernel" 
            let return(spr_valv) diskread.load_file(path, 0x100000) 
            *if result return(check) = true stop.exec:flow v_SYSTEM 
       }
}

[3.5] | {
       space diskread {
            fn load_file(path: asoc: int) <:path+%%> = struct {
                    success = true 

                    let fall = bios.read_file(path, asoc) path_hex 
                    return valv ( checkPlace = doc.func) 
            }
       }
}

[3.5] | {
       space terminal {
            fn dis(:bin(msg: opt)) {
                    bios.dis_msg
                    bios.dis = inp/opt>: pin_esc 
            }
       }
}
