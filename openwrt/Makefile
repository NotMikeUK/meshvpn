include $(TOPDIR)/rules.mk

# Name, version and release number
# The name and version of your package are used to define the variable to point to the build directory of your package: $(PKG_BUILD_DIR)
PKG_NAME:=meshvpn
PKG_VERSION:=2.0
PKG_RELEASE:=1
SOURCE_DIR:=..

include $(INCLUDE_DIR)/package.mk

# Package definition; instructs on how and where our package will appear in the overall configuration menu ('make menuconfig')
define Package/meshvpn
  SECTION:=network
  CATEGORY:=Network
  SUBMENU:=VPN
  TITLE:=MeshVPN
  DEPENDS:=+libopenssl +libstdcpp
endef
TARGET_LDFLAGS += -ldl -lcrypto -lssl

# Package description; a more verbose description on what our package does
define Package/meshvpn/description
  A simple mesh VPN daemon.
endef

# Package preparation instructions; create the build directory and copy the source code. 
# The last command is necessary to ensure our preparation instructions remain compatible with the patching system.
define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	cp $(SOURCE_DIR)/* $(PKG_BUILD_DIR)
	$(Build/Patch)
endef

# Package build instructions; invoke the target-specific compiler to first compile the source file, and then to link the file into the final executable
define Build/Compile
	$(TARGET_CXX) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/Crypto.o -c $(PKG_BUILD_DIR)/Crypto.cpp
	$(TARGET_CXX) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/MeshVPN.o -c $(PKG_BUILD_DIR)/MeshVPN.cpp
	$(TARGET_CXX) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/NetLink4.o -c $(PKG_BUILD_DIR)/NetLink4.cpp
	$(TARGET_CXX) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/NetLink6.o -c $(PKG_BUILD_DIR)/NetLink6.cpp
	$(TARGET_CXX) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/RemoteNode.o -c $(PKG_BUILD_DIR)/RemoteNode.cpp
	$(TARGET_CXX) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/RouteClient4.o -c $(PKG_BUILD_DIR)/RouteClient4.cpp
	$(TARGET_CXX) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/RouteClient6.o -c $(PKG_BUILD_DIR)/RouteClient6.cpp
	$(TARGET_CXX) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/RouteServer4Client.o -c $(PKG_BUILD_DIR)/RouteServer4Client.cpp
	$(TARGET_CXX) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/RouteServer4.o -c $(PKG_BUILD_DIR)/RouteServer4.cpp
	$(TARGET_CXX) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/RouteServer6Client.o -c $(PKG_BUILD_DIR)/RouteServer6Client.cpp
	$(TARGET_CXX) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/RouteServer6.o -c $(PKG_BUILD_DIR)/RouteServer6.cpp
	$(TARGET_CXX) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/Switch.o -c $(PKG_BUILD_DIR)/Switch.cpp
	$(TARGET_CXX) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/TunTap.o -c $(PKG_BUILD_DIR)/TunTap.cpp

	$(TARGET_CXX) $(TARGET_LDFLAGS) -o $(PKG_BUILD_DIR)/$1 $(PKG_BUILD_DIR)/*.o
endef

# Package install instructions; create a directory inside the package to hold our executable, and then copy the executable we built previously into the folder
define Package/meshvpn/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/meshvpn $(1)/usr/bin
endef

# This command is always the last, it uses the definitions and variables we give above in order to get the job done
$(eval $(call BuildPackage,meshvpn))