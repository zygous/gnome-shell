NULL = 
BUILT_SOURCES =
CLEANFILES =
EXTRA_DIST =
bin_SCRIPTS =
libexec_PROGRAMS =
noinst_LTLIBRARIES =
noinst_PROGRAMS =
service_in_files =

SUBDIRS = gvc

-include $(INTROSPECTION_MAKEFILE)
INTROSPECTION_GIRS =
INTROSPECTION_SCANNER_ARGS = --warn-all --warn-error --add-include-path=$(srcdir)
INTROSPECTION_COMPILER_ARGS = --includedir=$(srcdir) --includedir=$(MUTTER_TYPELIB_DIR)

typelibdir = $(pkglibdir)
typelib_DATA = $(INTROSPECTION_GIRS:.gir=.typelib)

servicedir = $(datadir)/dbus-1/services
service_DATA = $(service_in_files:.service.in=.service)

%.service: %.service.in Makefile
	$(AM_V_GEN)									\
		[ -d $(@D) ] || $(mkdir_p) $(@D) ;					\
		sed -e "s|\@libexecdir\@|$(libexecdir)|" $< > $@.tmp && mv $@.tmp $@
CLEANFILES += $(service_DATA)

CLEANFILES += $(gir_DATA) $(typelib_DATA)

bin_SCRIPTS += gnome-shell-extension-tool gnome-shell-perf-tool
EXTRA_DIST += gnome-shell-extension-tool.in gnome-shell-perf-tool.in
bin_PROGRAMS = gnome-shell gnome-shell-extension-prefs

generated_script_substitutions = \
	    -e "s|@bindir[@]|$(bindir)|g" \
	    -e "s|@datadir[@]|$(datadir)|g" \
	    -e "s|@libexecdir[@]|$(libexecdir)|g" \
	    -e "s|@libdir[@]|$(libdir)|g" \
	    -e "s|@pkglibdir[@]|$(pkglibdir)|g" \
	    -e "s|@pkgdatadir[@]|$(pkgdatadir)|g" \
	    -e "s|@PYTHON[@]|$(PYTHON)|g" \
	    -e "s|@VERSION[@]|$(VERSION)|g" \
	    -e "s|@sysconfdir[@]|$(sysconfdir)|g" \
	    -e "s|@GJS_CONSOLE[@]|$(GJS_CONSOLE)|g"

gnome-shell-extension-tool: gnome-shell-extension-tool.in Makefile
	$(AM_V_GEN) sed $(generated_script_substitutions) $< > $@.tmp && mv $@.tmp $@ && chmod a+x $@

gnome-shell-perf-tool: gnome-shell-perf-tool.in Makefile
	$(AM_V_GEN) sed $(generated_script_substitutions) $< > $@.tmp && mv $@.tmp $@ && chmod a+x $@

CLEANFILES += gnome-shell $(bin_SCRIPTS)

include Makefile-st.am
include Makefile-tray.am
include Makefile-calendar-server.am
include Makefile-hotplug-sniffer.am

gnome_shell_cflags =				\
	$(GNOME_SHELL_CFLAGS)			\
	-I$(srcdir)/tray			\
	-DVERSION=\"$(VERSION)\"		\
	-DLOCALEDIR=\"$(datadir)/locale\" 	\
	-DDATADIR=\"$(datadir)\"		\
	-DGNOME_SHELL_LIBEXECDIR=\"$(libexecdir)\"	\
	-DGNOME_SHELL_DATADIR=\"$(pkgdatadir)\"	\
	-DGNOME_SHELL_PKGLIBDIR=\"$(pkglibdir)\"

privlibdir = $(pkglibdir)
privlib_LTLIBRARIES = libgnome-shell-js.la libgnome-shell-menu.la libgnome-shell.la
noinst_LTLIBRARIES += libgnome-shell-base.la

shell_built_sources = \
	shell-enum-types.h \
	shell-enum-types.c

BUILT_SOURCES += $(shell_built_sources)

shell_public_headers_h =		\
	shell-app.h			\
	shell-app-system.h		\
	shell-app-usage.h		\
	shell-embedded-window.h		\
	shell-generic-container.h	\
	shell-glsl-quad.h		\
	shell-gtk-embed.h		\
	shell-global.h			\
	shell-invert-lightness-effect.h	\
	shell-keybinding-modes.h	\
	shell-mount-operation.h		\
	shell-perf-log.h		\
	shell-screenshot.h		\
	shell-slicer.h			\
	shell-stack.h			\
	shell-tp-client.h		\
	shell-tray-icon.h		\
	shell-tray-manager.h		\
	shell-util.h			\
	shell-window-tracker.h		\
	shell-wm.h

if HAVE_NETWORKMANAGER
shell_public_headers_h +=  shell-network-agent.h
endif

libgnome_shell_menu_la_SOURCES = 	\
	gtkactionmuxer.h		\
	gtkactionmuxer.c		\
	gtkactionobservable.h		\
	gtkactionobservable.c		\
	gtkactionobserver.h		\
	gtkactionobserver.c		\
	gtkmenutrackeritem.c		\
	gtkmenutrackeritem.h		\
	gtkmenutracker.c		\
	gtkmenutracker.h		\
	$(NULL)

libgnome_shell_base_la_SOURCES = 	\
	$(shell_public_headers_h)	\
	$(shell_private_sources)	\
	shell-embedded-window-private.h	\
	shell-embedded-window.c		\
	shell-generic-container.c	\
	shell-glsl-quad.c		\
	shell-invert-lightness-effect.c	\
	shell-keyring-prompt.h		\
	shell-keyring-prompt.c		\
	shell-menu-tracker.c		\
	shell-menu-tracker.h		\
	shell-mount-operation.c		\
	shell-perf-log.c		\
	shell-polkit-authentication-agent.h	\
	shell-polkit-authentication-agent.c	\
	shell-secure-text-buffer.c	\
	shell-secure-text-buffer.h	\
	shell-slicer.c			\
	shell-stack.c			\
	shell-tp-client.c		\
	$(NULL)

if HAVE_NETWORKMANAGER
libgnome_shell_base_la_SOURCES +=  shell-network-agent.c
endif

libgnome_shell_sources =		\
	$(shell_public_headers_h)	\
	shell-app-private.h		\
	shell-app-system-private.h	\
	shell-global-private.h		\
	shell-window-tracker-private.h	\
	shell-wm-private.h		\
	gnome-shell-plugin.c		\
	shell-app.c			\
	shell-app-system.c		\
	shell-app-usage.c		\
	shell-global.c			\
	shell-gtk-embed.c		\
	shell-screenshot.c		\
	shell-tray-icon.c		\
	shell-tray-manager.c		\
	shell-util.c			\
	shell-window-tracker.c		\
	shell-wm.c			\
	$(NULL)

libgnome_shell_built_sources =		\
	$(shell_built_sources)		\
	$(top_builddir)/js/js-resources.c		\
	$(top_builddir)/js/js-resources.h		\
	$(NULL)

libgnome_shell_la_SOURCES = $(libgnome_shell_sources)
nodist_libgnome_shell_la_SOURCES = $(libgnome_shell_built_sources)

libgnome_shell_la_gir_sources = \
	$(filter-out %-private.h $(shell_private_sources), $(shell_public_headers_h) $(libgnome_shell_base_la_SOURCES) $(libgnome_shell_sources) $(libgnome_shell_built_sources))

gnome_shell_SOURCES = main.c
gnome_shell_CPPFLAGS = \
	-DMUTTER_TYPELIB_DIR=\"$(MUTTER_TYPELIB_DIR)\" \
	$(MUTTER_CFLAGS) \
	$(gnome_shell_cflags)

# Here, and after, we repeat mutter and bluetooth libraries just for the rpath
# The dependency is already pulled in by libtool
gnome_shell_LDADD = libgnome-shell.la libgnome-shell-js.la $(GNOME_SHELL_LIBS) $(MUTTER_LIBS)
gnome_shell_DEPENDENCIES = libgnome-shell.la

gnome_shell_extension_prefs_SOURCES = \
	gnome-shell-extension-prefs.c \
	$(NULL)
nodist_gnome_shell_extension_prefs_SOURCES = \
	$(top_builddir)/js/js-resources.c		\
	$(top_builddir)/js/js-resources.h		\
	$(NULL)
gnome_shell_extension_prefs_CPPFLAGS = $(gnome_shell_cflags)
gnome_shell_extension_prefs_LDADD = libgnome-shell-js.la $(GNOME_SHELL_LIBS)

if HAVE_NETWORKMANAGER

libexec_PROGRAMS += gnome-shell-portal-helper
gnome_shell_portal_helper_SOURCES = \
	gnome-shell-portal-helper.c \
	$(NULL)
nodist_gnome_shell_portal_helper_SOURCES = \
	$(top_builddir)/js/js-resources.c		\
	$(top_builddir)/js/js-resources.h		\
	$(NULL)
gnome_shell_portal_helper_CPPFLAGS = $(gnome_shell_cflags)
gnome_shell_portal_helper_LDADD = libgnome-shell-js.la $(GNOME_SHELL_LIBS)

endif

########################################

libgnome_shell_js_la_SOURCES =		\
	shell-js.h			\
	shell-js.cpp			\
	$(NULL)

libgnome_shell_js_la_LIBADD =		\
	$(GNOME_SHELL_JS_LIBS)		\
	$(NULL)

libgnome_shell_js_la_LDFLAGS =		\
	-avoid-version

libgnome_shell_js_la_CPPFLAGS =		\
	$(GNOME_SHELL_JS_CFLAGS)

########################################

shell_recorder_sources =        \
	shell-recorder.c	\
	shell-recorder.h

# Custom element is an internal detail

if BUILD_RECORDER
libgnome_shell_sources += $(shell_recorder_sources)

shell_recorder_private_sources =  \
	shell-recorder-src.c	\
	shell-recorder-src.h	\
	$(NULL)

shell_private_sources = $(shell_recorder_private_sources)

endif BUILD_RECORDER

########################################

libexec_PROGRAMS += gnome-shell-perf-helper

gnome_shell_perf_helper_SOURCES = shell-perf-helper.c
gnome_shell_perf_helper_CPPFLAGS = $(SHELL_PERF_HELPER_CFLAGS)
gnome_shell_perf_helper_LDADD = $(SHELL_PERF_HELPER_LIBS) -lm

########################################

noinst_PROGRAMS += run-js-test

run_js_test_CPPFLAGS = $(MUTTER_CFLAGS) $(gnome_shell_cflags)
run_js_test_LDADD = libgnome-shell.la $(GNOME_SHELL_JS_LIBS) $(MUTTER_LIBS)
run_js_test_LDFLAGS = -export-dynamic

run_js_test_SOURCES =			\
	run-js-test.c

########################################

shell-enum-types.h: stamp-shell-enum-types.h Makefile
	@true
stamp-shell-enum-types.h: $(srcdir)/shell-enum-types.h.in $(shell_public_headers_h)
	$(AM_V_GEN) ( \
	  $(GLIB_MKENUMS) \
	    --template $< \
	  $(addprefix $(srcdir)/,$(shell_public_headers_h)) ) > $(@F).tmp && \
	(cmp -s $(@F).tmp shell-enum-types.h || mv $(@F).tmp shell-enum-types.h) && \
	rm -f $(@F).tmp && \
	echo timestamp > $(@F)
EXTRA_DIST += shell-enum-types.h.in
CLEANFILES += stamp-shell-enum-types.h

shell-enum-types.c: $(srcdir)/shell-enum-types.c.in stamp-shell-enum-types.h
	$(AM_V_GEN) ( \
	  $(GLIB_MKENUMS) \
	    --template $< \
	  $(addprefix $(srcdir)/,$(shell_public_headers_h)) ) > $(@F).tmp && \
	mv $(@F).tmp $(@F) && \
	rm -f $(@F).tmp
EXTRA_DIST += shell-enum-types.c.in

libgnome_shell_ldflags = -avoid-version
libgnome_shell_libadd =		\
	-lm			\
	$(GNOME_SHELL_LIBS)	\
	libgnome-shell-menu.la	\
	libst-1.0.la       	\
	libtray.la		\
	gvc/libgvc.la		\
	$(NULL)

libgnome_shell_menu_la_LDFLAGS = $(libgnome_shell_ldflags)
libgnome_shell_menu_la_LIBADD = $(GNOME_SHELL_LIBS)
libgnome_shell_menu_la_CPPFLAGS = $(GNOME_SHELL_CFLAGS)

libgnome_shell_base_la_LIBADD = $(libgnome_shell_libadd)
libgnome_shell_base_la_CPPFLAGS = $(gnome_shell_cflags)

libgnome_shell_la_LDFLAGS = $(libgnome_shell_ldflags)
libgnome_shell_la_LIBADD = $(GNOME_SHELL_LIBS) $(MUTTER_LIBS) libgnome-shell-base.la
libgnome_shell_la_CPPFLAGS = $(MUTTER_CFLAGS) $(gnome_shell_cflags)

ShellMenu-0.1.gir: libgnome-shell-menu.la
ShellMenu_0_1_gir_INCLUDES = Gio-2.0
ShellMenu_0_1_gir_CFLAGS = $(libgnome_shell_menu_la_CPPFLAGS) -I $(srcdir)
ShellMenu_0_1_gir_LIBS = libgnome-shell-menu.la
ShellMenu_0_1_gir_FILES = \
	gtkactionmuxer.h		\
	gtkactionmuxer.c		\
	gtkactionobservable.h		\
	gtkactionobservable.c		\
	gtkactionobserver.h		\
	gtkactionobserver.c		\
	gtkmenutrackeritem.c		\
	gtkmenutrackeritem.h		\
	$(NULL)
ShellMenu_0_1_gir_SCANNERFLAGS = 	\
	--namespace=ShellMenu --identifier-prefix=Gtk
INTROSPECTION_GIRS += ShellMenu-0.1.gir
CLEANFILES += ShellMenu-0.1.gir

Shell-0.1.gir: gnome-shell St-1.0.gir ShellMenu-0.1.gir
Shell_0_1_gir_INCLUDES = Clutter-1.0 ClutterX11-1.0 Meta-3.0 TelepathyGLib-0.12 Soup-2.4
if HAVE_NETWORKMANAGER
Shell_0_1_gir_INCLUDES += NetworkManager-1.0 NMClient-1.0
endif
Shell_0_1_gir_CFLAGS = $(libgnome_shell_la_CPPFLAGS) -I $(srcdir)
Shell_0_1_gir_LIBS = libgnome-shell.la
Shell_0_1_gir_FILES = $(libgnome_shell_la_gir_sources)
Shell_0_1_gir_SCANNERFLAGS =	\
	--include-uninstalled=$(builddir)/St-1.0.gir \
	--include-uninstalled=$(builddir)/ShellMenu-0.1.gir \
	--add-include-path=$(MUTTER_GIR_DIR)
INTROSPECTION_GIRS += Shell-0.1.gir
CLEANFILES += Shell-0.1.gir

ShellJS-0.1.gir: libgnome-shell-js.la
ShellJS_0_1_gir_CFLAGS = $(libgnome_shell_la_CPPFLAGS) -I $(srcdir)
ShellJS_0_1_gir_LIBS = libgnome-shell-js.la
ShellJS_0_1_gir_FILES = $(libgnome_shell_js_la_SOURCES)
INTROSPECTION_GIRS += ShellJS-0.1.gir
CLEANFILES += ShellJS-0.1.gir

St-1.0.gir: libst-1.0.la
St_1_0_gir_INCLUDES = Clutter-1.0 Gtk-3.0
St_1_0_gir_CFLAGS = $(st_cflags) -DST_COMPILATION
St_1_0_gir_LIBS = libst-1.0.la
St_1_0_gir_FILES = $(filter-out %-private.h $(st_non_gir_sources), $(addprefix $(srcdir)/,$(st_source_h))) \
	$(addprefix $(srcdir)/,$(st_source_c))
INTROSPECTION_GIRS += St-1.0.gir
CLEANFILES += St-1.0.gir
