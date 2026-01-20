pkglib_LTLIBRARIES = eglplatform_membrane.la

EXTRA_DIST = linux-dmabuf-v1.xml

BUILT_SOURCES = linux-dmabuf-v1-protocol.c \
		linux-dmabuf-v1-client-protocol.h

%-protocol.c : %.xml
	$(AM_V_GEN)$(WAYLAND_SCANNER) private-code < $< > $@

%-client-protocol.h : %.xml
	$(AM_V_GEN)$(WAYLAND_SCANNER) client-header < $< > $@

eglplatform_membrane_la_SOURCES = eglplatform_membrane.cpp linux-dmabuf-v1-protocol.c
eglplatform_membrane_la_CXXFLAGS = \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/common \
	-I$(top_srcdir)/platforms/common \
	-I$(top_srcdir)/common \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/egl \
	-I$(top_srcdir)/egl/platforms/common \
	$(ANDROID_HEADERS_CFLAGS) \
	$(WAYLAND_SERVER_CFLAGS) \
	$(WAYLAND_CLIENT_CFLAGS) \
	$(WAYLAND_EGL_CFLAGS) \
	$(LIBDRM_CFLAGS)

eglplatform_membrane_la_LDFLAGS = \
	-avoid-version -module -shared -export-dynamic \
	$(top_builddir)/egl/platforms/common/libhybris-eglplatformcommon.la \
	$(top_builddir)/platforms/common/libhybris-platformcommon.la \
	$(top_builddir)/gralloc/libgralloc.la \
	$(WAYLAND_SERVER_LIBS) \
	$(WAYLAND_CLIENT_LIBS) \
	$(WAYLAND_EGL_LIBS)

if WANT_DEBUG
eglplatform_membrane_la_CXXFLAGS += -I$(top_srcdir)/common -ggdb -O0
endif

if WANT_TRACE
eglplatform_membrane_la_CXXFLAGS += -DDEBUG
endif
