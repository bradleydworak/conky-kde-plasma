# conky-kde-plasma
Conky v1.12 configuration example with custom colors for KDE Plasma 5

Displays information for AMD CPU, NVIDIA GPU, APC Backup, and USB devices
```
conky.config = {
    own_window = true,
    own_window_class = 'Conky',
    --own_window_type = 'dock',
    --own_window_type = 'desktop',
    own_window_type = 'normal',
    own_window_transparent = false,
    own_window_hints = 'below,skip_taskbar,sticky',
    own_window_argb_visual = true,
    own_window_argb_value = 145,
    double_buffer = true,
    alignment = 'top_right',
    background = false,
    border_width = 1,
    cpu_avg_samples = 2,
    default_color = 'white',
    default_outline_color = 'white',
    default_shade_color = 'white',
    double_buffer = true,
    draw_borders = false,
    draw_graph_borders = true,
    draw_outline = false,
    draw_shades = false,
    extra_newline = false,
    font = 'DejaVu Sans Mono:size=12',
    gap_x = 60,
    gap_y = 60,
    minimum_height = 5,
    minimum_width = 5,
    net_avg_samples = 2,
    no_buffers = true,
    out_to_console = false,
    out_to_ncurses = false,
    out_to_stderr = false,
    out_to_x = true,   
    show_graph_range = false,
    show_graph_scale = false,
    stippled_borders = 0,
    update_interval = 1.0,
    uppercase = false,
    use_spacer = 'none',
    use_xft = true,
    color1 = '1EB5FF',
    color2 = '98FF76',
    color3 = '0090ff',
    color4 = '30DDFB',
}

conky.text = [[
    ${color grey}Info:$color ${scroll 32 Conky $conky_version - $sysname $nodename $kernel $machine}
    $hr
    ${color orange}${execi 1000 lscpu | grep 'Model name' | cut -f 2 -d ":" | awk '{$1=$1}1'}
    ${color grey}Uptime:$color $uptime
    ${color grey}CPU Frequency (in GHz):$color $freq_g
    ${color grey}GPU Frequency (in MHz):$color ${nvidia gpufreq}
    ${color grey}RAM Usage:$color $mem/$memmax - $memperc% ${membar 4}
    ${color grey}Swap Usage:$color $swap/$swapmax - $swapperc% ${swapbar 4}
    ${color grey}CPU Usage:$color $cpu% ${cpubar 4}
    ${color grey}Nvme Temp:$color ${hwmon temp 1}°C
    ${color4}GPU Temp:$color ${nvidia temp}°C
    ${color4}GPU Power:$color ${texeci 5 nvidia-smi -i 0 -q -d POWER | grep -m 1 "Power Draw" | grep -Eo '[0-9]{1,3}.[0-9]{1,3} [W]'}
    ${color4}GPU Fan Speed: $color${texeci 5 nvidia-smi --query-gpu=fan.speed --format=csv,noheader,nounits} rpm
    ${color4}CPU Temp:$color ${hwmon 1 temp 1}°C
    $hr
    ${color1}APC${apcupsd localhost 3551} ${apcupsd_model}
    ${color grey}Status: $color${apcupsd_status}
    ${color grey}Battery Time: ${apcupsd_timeleft}m
    ${color grey}Load: ${apcupsd_load}% ${apcupsd_loadbar}
    $hr
    ${color2}USB Devices : ${execpi 5 lsusb | grep -iv 'hub' | cut --fields=7- --delimiter=' ' | wc -l} 
    ${color grey}${execpi 5 lsusb | grep -iv 'hub' | cut --fields=7- --delimiter=' '}
    $hr
    ${color grey}Processes:$color $processes  ${color grey}Running:$color $running_processes
    ${color grey}Threads:$color $threads  ${color grey}Running:$color $running_threads
    ${color4}External IP: $color${execi 3600 wget -q -O- http://ipecho.net/plain}
    $hr
    ${color1}File systems:
    $color${fs_used /}/${fs_size /} ${fs_bar 6 /}
    ${color1}Networking:
    ${color grey}Up:$color ${upspeed} ${color grey} - Down:$color ${downspeed}
    ${color grey}Total Up: $color${totalup eno1} ${color grey}Total Down: $color${totaldown eno1}
    $hr
    ${color grey}Name              PID     CPU%   MEM%
    ${color lightgrey} ${top name 1} ${top pid 1} ${top cpu 1} ${top mem 1}
    ${color lightgrey} ${top name 2} ${top pid 2} ${top cpu 2} ${top mem 2}
    ${color lightgrey} ${top name 3} ${top pid 3} ${top cpu 3} ${top mem 3}
    ${color lightgrey} ${top name 4} ${top pid 4} ${top cpu 4} ${top mem 4}
]]
```
