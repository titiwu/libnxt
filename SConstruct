from glob import glob

auto_libs = ''

BuildEnv = Environment(CCFLAGS=['-Wall', '-std=gnu99',
				'-g', '-ggdb', '-D' + endian])
if auto_libs:
	BuildEnv.ParseConfig('pkg-config --cflags --libs ' + auto_libs)

BuildEnv.Command('flash_routine.h',
		 'flash_routine.h.base',
		 'python2 make_flash_header.py')

Default(BuildEnv.Library('nxt',
			 [x for x in glob('*.c')
			  if not x.startswith('main_')],
			 LIBS='usb'))

Default(BuildEnv.Program('fwflash', 'main_fwflash.c',
			 LIBS=['usb', 'nxt'], LIBPATH='.'))

Default(BuildEnv.Program('fwexec', 'main_fwexec.c',
			 LIBS=['usb', 'nxt'], LIBPATH='.'))
