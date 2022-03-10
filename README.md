env PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install --force 3.6.9 -v
pyenv global 3.6.9

python -m pip install meson
python -m pip install ninja

git clone -b 1.20 https://gitlab.freedesktop.org/gstreamer/gstreamer.git
cd gstreamer
sudo apt install -y flex bison libglib2.0-dev libgirepository1.0-dev libvpx-dev libsrtp-dev libsrtp2-dev libcairo2-dev libcairo-gobject2 libva-dev libdrm-dev i965-va-driver

export DISPLAY=:0

meson builddir \
  --buildtype=release \
  --strip \
  -Dauto_features=disabled \
  -Dpython=enabled \
  -Dintrospection=enabled \
  -Dpygobject:pycairo=enabled \
  -Dlibnice=enabled \
  -Dlibnice:gstreamer=enabled \
  -Dgstreamer:tools=enabled \
  -Dvaapi=enabled \
  -Dgst-plugins-base:videotestsrc=enabled \
  -Dgst-plugins-base:app=enabled \
  -Dgood=enabled \
  -Dgst-plugins-good:vpx=enabled \
  -Dgst-plugins-good:rtp=enabled \
  -Dgst-plugins-good:rtpmanager=enabled \
  -Dgst-plugins-good:rtsp=enabled \
  -Dgst-plugins-good:udp=enabled \
  -Dgst-plugins-good:multifile=enabled \
  -Dgst-plugins-good:isomp4=enabled \
  -Dgst-plugins-good:autodetect=enabled \
  -Dbad=enabled \
  -Dgst-plugins-bad:proxy=enabled \
  -Dgst-plugins-bad:videoparsers=enabled \
  -Dgst-plugins-bad:rtp=enabled \
  -Dgst-plugins-bad:dtls=enabled \
  -Dgst-plugins-bad:srtp=enabled \
  -Dgst-plugins-bad:sctp=enabled \
  -Dgst-plugins-bad:webrtc=enabled

ninja -C builddir

python /home/ubuntu/gstreamer/gst-env.py --builddir=/home/ubuntu/gstreamer/builddir --gstbuilddir=/home/ubuntu/gstreamer/builddir --srcdir=/home/ubuntu/gstreamer



//////
full guide
//////
git clone -b 1.20 https://gitlab.freedesktop.org/gstreamer/gstreamer.git


// OpenGL
sudo apt install libglu1-mesa-dev freeglut3-dev mesa-common-dev

//install glib
sudo apt instalninja -C build-gst-full
or
wget https://download.gnome.org/sources/glib/2.70/glib-2.70.4.tar.xz
tar -xf glib-2.70.4.tar.xz
cd glib-2.70.4
meson builddir
ninja -C builddir
sudo $(which ninja) -C builddir install

//gobject-introspection
sudo apt install -y libgirepository1.0-dev

// libvpx-dev
sudo apt install -y libvpx-dev

//libsrtp
sudo apt install -y libsrtp-dev libsrtp2-dev

//cairo 
sudo apt install -y libcairo2-dev libcairo-gobject2
or
git clone https://gitlab.freedesktop.org/cairo/cairo.git
cd cairo
meson builddir
ninja -C builddir
sudo $(which ninja) -C builddir install

//libva
sudo apt install -y libdrm-dev
git clone https://github.com/intel/libva.git
cd libva
meson builddir
ninja -C builddir
sudo $(which ninja) -C builddir install

//i965 driver
export LIBVA_DRIVER_NAME=i965
export LIBVA_DRIVERS_PATH=/usr/lib/x86_64-linux-gnu/dri
git clone https://github.com/intel/intel-vaapi-driver.git
cd intel-vaapi-driver/
meson builddir --prefix=/usr --buildtype=release
ninja -C builddir
sudo $(which ninja) -C builddir install

//vainfo (optional)
sudo apt install -y vainfo
or
git clone https://github.com/intel/libva-utils.git
cd libva-utils
meson builddir
ninja -C builddir
sudo $(which ninja) -C builddir install


meson builddir \
  --buildtype=release \
  --strip \
  -Dauto_features=disabled \
  -Dpython=enabled \
  -Dintrospection=enabled \
  -Dpygobject:pycairo=enabled \
  -Dlibnice=enabled \
  -Dlibnice:gstreamer=enabled \
  -Dgstreamer:tools=enabled \
  -Dvaapi=enabled \
  -Dgst-plugins-base:videotestsrc=enabled \
  -Dgst-plugins-base:app=enabled \
  -Dgood=enabled \
  -Dgst-plugins-good:vpx=enabled \
  -Dgst-plugins-good:rtp=enabled \
  -Dgst-plugins-good:rtpmanager=enabled \
  -Dgst-plugins-good:rtsp=enabled \
  -Dgst-plugins-good:udp=enabled \
  -Dgst-plugins-good:multifile=enabled \
  -Dgst-plugins-good:isomp4=enabled \
  -Dgst-plugins-good:autodetect=enabled \
  -Dbad=enabled \
  -Dgst-plugins-bad:proxy=enabled \
  -Dgst-plugins-bad:videoparsers=enabled \
  -Dgst-plugins-bad:rtp=enabled \
  -Dgst-plugins-bad:dtls=enabled \
  -Dgst-plugins-bad:srtp=enabled \
  -Dgst-plugins-bad:sctp=enabled \
  -Dgst-plugins-bad:webrtc=enabled

ninja -C builddir
