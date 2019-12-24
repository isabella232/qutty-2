
MSVC_ROOT_DIR="C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Tools\MSVC\14.23.28105"
WKIT_ROOT_DIR="C:\Program Files (x86)\Windows Kits\10"

#/nologo 
CFLAGS = -I$(WKIT_ROOT_DIR)\Include\10.0.18362.0\ucrt \
         -I$(WKIT_ROOT_DIR)\Include\10.0.18362.0\um \
         -I$(WKIT_ROOT_DIR)\Include\10.0.18362.0\shared \
         -I$(MSVC_ROOT_DIR)\include  \
         -I..\./ -I..\charset/ -I..\windows/ -I..\unix/ \
         /W3 /O1 \
         /D_WINDOWS /D_WIN32_WINDOWS=0x500 /DWINVER=0x500 /D_CRT_SECURE_NO_WARNINGS

LFLAGS = /LIBPATH:$(WKIT_ROOT_DIR)\Lib\10.0.18362.0\ucrt\x64 \
         /LIBPATH:$(WKIT_ROOT_DIR)\Lib\10.0.18362.0\um\x64 \
         /LIBPATH:$(MSVC_ROOT_DIR)\lib\x64 \
         /incremental:no /dynamicbase /nxcompat

RCFLAGS = -I$(WKIT_ROOT_DIR)\Include\10.0.18362.0\um \
          -I$(WKIT_ROOT_DIR)\Include\10.0.18362.0\shared \
          -I..\./ -I..\charset/ -I..\windows/ -I..\unix/ \
          -DWIN32 -D_WIN32 -DWINVER=0x0400

CFLAGS = $(CFLAGS) /DHAS_GSSAPI


PUTTY_OBJS= $(BUILDDIR)aqsync.obj \
        $(BUILDDIR)be_all_s.obj \
		$(BUILDDIR)be_misc.obj \
        $(BUILDDIR)callback.obj \
		$(BUILDDIR)cmdline.obj \
        $(BUILDDIR)conf.obj \
		$(BUILDDIR)config.obj \
        $(BUILDDIR)cproxy.obj \
		$(BUILDDIR)dialog.obj \
        $(BUILDDIR)errsock.obj \
		$(BUILDDIR)ldisc.obj \
        $(BUILDDIR)ldiscucs.obj \
		$(BUILDDIR)logging.obj \
        $(BUILDDIR)minibidi.obj \
		$(BUILDDIR)misc.obj \
        $(BUILDDIR)miscucs.obj \
		$(BUILDDIR)pgssapi.obj \
        $(BUILDDIR)pinger.obj \
		$(BUILDDIR)portfwd.obj \
        $(BUILDDIR)proxy.obj \
		$(BUILDDIR)putty.res \
        $(BUILDDIR)raw.obj \
		$(BUILDDIR)rlogin.obj \
        $(BUILDDIR)sercfg.obj \
		$(BUILDDIR)settings.obj \
        $(BUILDDIR)sizetip.obj \
		$(BUILDDIR)ssh.obj \
        $(BUILDDIR)sshaes.obj \
		$(BUILDDIR)ssharcf.obj \
        $(BUILDDIR)sshblowf.obj \
		$(BUILDDIR)sshbn.obj \
        $(BUILDDIR)sshccp.obj \
		$(BUILDDIR)sshcrc.obj \
        $(BUILDDIR)sshcrcda.obj \
		$(BUILDDIR)sshdes.obj \
        $(BUILDDIR)sshdh.obj \
		$(BUILDDIR)sshdss.obj \
        $(BUILDDIR)sshecc.obj \
		$(BUILDDIR)sshgssc.obj \
        $(BUILDDIR)sshmd5.obj \
		$(BUILDDIR)sshpubk.obj \
        $(BUILDDIR)sshrand.obj \
		$(BUILDDIR)sshrsa.obj \
        $(BUILDDIR)sshsh256.obj \
		$(BUILDDIR)sshsh512.obj \
        $(BUILDDIR)sshsha.obj \
		$(BUILDDIR)sshshare.obj \
        $(BUILDDIR)sshzlib.obj \
		$(BUILDDIR)telnet.obj \
        $(BUILDDIR)terminal.obj \
		$(BUILDDIR)timing.obj \
        $(BUILDDIR)tree234.obj \
		$(BUILDDIR)version.obj \
        $(BUILDDIR)wcwidth.obj \
		$(BUILDDIR)wildcard.obj \
        $(BUILDDIR)wincapi.obj \
		$(BUILDDIR)wincfg.obj \
        $(BUILDDIR)winctrls.obj \
		$(BUILDDIR)windefs.obj \
        $(BUILDDIR)windlg.obj \
		$(BUILDDIR)window.obj \
        $(BUILDDIR)wingss.obj \
		$(BUILDDIR)winhandl.obj \
        $(BUILDDIR)winhelp.obj \
		$(BUILDDIR)winhsock.obj \
        $(BUILDDIR)winjump.obj \
		$(BUILDDIR)winmisc.obj \
        $(BUILDDIR)winnet.obj \
		$(BUILDDIR)winnoise.obj \
        $(BUILDDIR)winnpc.obj \
		$(BUILDDIR)winnps.obj \
        $(BUILDDIR)winpgntc.obj \
		$(BUILDDIR)winprint.obj \
        $(BUILDDIR)winproxy.obj \
		$(BUILDDIR)winsecur.obj \
        $(BUILDDIR)winser.obj \
		$(BUILDDIR)winshare.obj \
        $(BUILDDIR)winstore.obj \
		$(BUILDDIR)wintime.obj \
        $(BUILDDIR)winucs.obj \
		$(BUILDDIR)winutils.obj \
        $(BUILDDIR)winx11.obj \
		$(BUILDDIR)x11fwd.obj

STATIC_LIB = advapi32.lib \
             comctl32.lib \
             comdlg32.lib \
             gdi32.lib \
             imm32.lib \
             ole32.lib \
             shell32.lib \
             user32.lib \
             winmm.lib \
             winspool.lib 
      
all: $(BUILDDIR)putty.exe

$(BUILDDIR)putty.exe: $(PUTTY_OBJS)
	link $(LFLAGS) $(XLFLAGS) -out:$(BUILDDIR)putty.exe \
         -map:$(BUILDDIR)putty.map \
         -subsystem:windows$(SUBSYSVER) \
         $(STATIC_LIB) $(PUTTY_OBJS)

$(BUILDDIR)putty.res: ..\windows\putty.rc ..\windows\rcstuff.h \
		..\windows\win_res.rc2 ..\windows\putty.mft \
		..\windows\win_res.h ..\windows\putty.ico \
		..\windows\puttycfg.ico ..\windows\version.rc2 ..\version.h \
		..\licence.h
	rc /Fo$(BUILDDIR)putty.res $(RCFL) -r $(RCFLAGS) ..\windows\putty.rc

.c.obj::
	cl /Fo$(BUILDDIR) $(COMPAT) $(CFLAGS) $(XFLAGS) /c $<

{..\}.c.obj::
	cl /Fo$(BUILDDIR) $(COMPAT) $(CFLAGS) $(XFLAGS) /c $<

{..\charset\}.c.obj::
	cl /Fo$(BUILDDIR) $(COMPAT) $(CFLAGS) $(XFLAGS) /c $<

{..\windows\}.c.obj::
	cl /Fo$(BUILDDIR) $(COMPAT) $(CFLAGS) $(XFLAGS) /c $<

{..\unix\}.c.obj::
	cl /Fo$(BUILDDIR) $(COMPAT) $(CFLAGS) $(XFLAGS) /c $<

clean: tidy
	-del $(BUILDDIR)*.exe

tidy:
	-del $(BUILDDIR)*.obj
	-del $(BUILDDIR)*.res
	-del $(BUILDDIR)*.pch
	-del $(BUILDDIR)*.aps
	-del $(BUILDDIR)*.ilk
	-del $(BUILDDIR)*.pdb
	-del $(BUILDDIR)*.rsp
	-del $(BUILDDIR)*.dsp
	-del $(BUILDDIR)*.dsw
	-del $(BUILDDIR)*.ncb
	-del $(BUILDDIR)*.opt
	-del $(BUILDDIR)*.plg
	-del $(BUILDDIR)*.map
	-del $(BUILDDIR)*.idb
	-del $(BUILDDIR)debug.log
