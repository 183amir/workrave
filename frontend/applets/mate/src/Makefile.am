if HAVE_MATE

WORKRAVE_MENU_UI_DIR = $(datadir)/mate-panel/ui

libappletdir = $(libdir)/mate-applets
libapplet_PROGRAMS = workrave-applet

APPLET_LOCATION = ${libappletdir}/workrave-applet

workrave_applet_SOURCES = main.c

workrave_applet_CFLAGS =	-Wall -std=c99 -DPANEL_MATE \
				@WR_COMMON_INCLUDES@ @WR_BACKEND_INCLUDES@ @WR_FRONTEND_COMMON_INCLUDES@ \
				-I$(srcdir)/../include -I$(srcdir)/../../common/include \
				$(LIBMATEPANEL_CFLAGS) \
				-DMATELOCALEDIR=\""$(datadir)/locale"\" \
	  	  		-DWORKRAVE_PKGDATADIR="\"${pkgdatadir}\"" \
				-DWORKRAVE_MENU_UI_DIR="\"${WORKRAVE_MENU_UI_DIR}"\"

workrave_applet_LDADD = 	$(LIBMATEPANEL_LIBS) $(LIBMATEGUI4_LIBS) $(LIBMATEPANEL_LIBS) \
			        @GTK2_LIBS@ -L$(builddir)/../../common/src -lworkrave-gtk2-private-1.0


appletsdir       = $(datadir)/mate-panel/applets
applets_in_files = org.workrave.WorkraveApplet.mate-panel-applet.in
applets_DATA     = $(applets_in_files:.mate-panel-applet.in=.mate-panel-applet)

$(applets_in_files): $(applets_in_files).in Makefile
	$(AM_V_GEN)sed \
		-e "s|\@LOCATION\@|$(APPLET_LOCATION)|" \
		$< > $@
%.mate-panel-applet: %.mate-panel-applet.in $(INTLTOOL_MERGE) $(wildcard $(top_srcdir)/po/*po) ; $(INTLTOOL_MERGE) $(top_srcdir)/po $< $@ -d -u -c $(top_builddir)/po/.intltool-merge-cache

servicedir       = $(datadir)/dbus-1/services
service_in_files = org.mate.panel.applet.WorkraveAppletFactory.service.in
service_DATA     = $(service_in_files:.service.in=.service)

org.mate.panel.applet.WorkraveAppletFactory.service: $(service_in_files)
	$(AM_V_GEN)sed \
		-e "s|\@LOCATION\@|$(APPLET_LOCATION)|" \
		$< > $@


xmluidir   = $(WORKRAVE_MENU_UI_DIR)
xmlui_DATA = workrave-menu.xml

CLEANFILES = $(applet_DATA) $(applet_DATA).in $(service_DATA)

EXTRA_DIST = \
	org.workrave.WorkraveApplet.mate-panel-applet.in.in \
	$(applets_in_files) \
	$(service_in_files) \
        $(xmlui_DATA)
endif
