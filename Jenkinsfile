// Jenkins Pipeline - vscodium deb packager - riscv64
//

pipeline {
   agent { label 'pioneer' }

   environment {
        //
        PKG_VERSION='1.94.0.24281'
        PKG_ITERATION='1'
        ARCH = 'riscv64'
        // weblinks
        DEB_WEBLINK="https://github.com/VSCodium/vscodium/releases/download/${PKG_VERSION}/codium_${PKG_VERSION}_arm64.deb"
        CODIUM_WEBLINK="https://github.com/VSCodium/vscodium/releases/download/${PKG_VERSION}/VSCodium-linux-riscv64-${PKG_VERSION}.tar.gz"
        //
   }
   stages {
      stage('Clean Workspace') {
         steps {
            echo 'Cleaning Workspace'
            cleanWs()
            script {
                    currentBuild.displayName = "codium-${PKG_VERSION}-${PKG_ITERATION}"
                }
         }
      }
      stage('Get VSCodium') {
         steps {
            echo 'Getting VSCodium'
            sh 'curl -fsSL "$DEB_WEBLINK" -o codium.deb'
            sh 'curl -fsSL "$CODIUM_WEBLINK" -o vscodium.tar.gz'
         }
      }
      stage('Expand Packages') {
          steps {
            sh 'ar -x codium.deb'
            sh 'tar -xf data.tar.xz'
            sh 'tar -xf control.tar.xz'
            sh 'ls'
            sh 'rm -rf usr/share/codium/*'
            sh 'tar -xzf vscodium.tar.gz -C usr/share/codium'
          }
      }
      stage('Package DEB') {
          steps {
            echo "building deb"
            sh "rm *.deb || true"
            sh "export XZ_DEFAULTS='-7 -T0'; fpm \
               -s dir \
               -t deb \
               -a ${ARCH} \
               --name codium \
               --version ${PKG_VERSION} \
               --iteration ${PKG_ITERATION} \
               -d 'ca-certificates' \
               -d 'libasound2 (>= 1.0.17)' \
               -d 'libatk-bridge2.0-0 (>= 2.5.3)' \
               -d 'libatk1.0-0 (>= 2.2.0)' \
               -d 'libatspi2.0-0 (>= 2.9.90)' \
               -d 'libc6 (>= 2.17)' \
               -d 'libcairo2 (>= 1.6.0)' \
               -d 'libcups2 (>= 1.6.0)' \
               -d 'libcurl3-gnutls | libcurl3-nss | libcurl4 | libcurl3' \
               -d 'libdbus-1-3 (>= 1.9.14)' \
               -d 'libdrm2 (>= 2.4.75)' \
               -d 'libexpat1 (>= 2.1~beta3)' \
               -d 'libgbm1 (>= 17.1.0~rc2)' \
               -d 'libglib2.0-0 (>= 2.37.3)' \
               -d 'libgssapi-krb5-2 (>= 1.17)' \
               -d 'libgtk-3-0 (>= 3.9.10)' \
               -d 'libgtk-3-0 (>= 3.9.10) | libgtk-4-1' \
               -d 'libkrb5-3 (>= 1.6.dfsg.2)' \
               -d 'libnspr4 (>= 2:4.9-2~)' \
               -d 'libnss3 (>= 2:3.30)' \
               -d 'libnss3 (>= 3.26)' \
               -d 'libpango-1.0-0 (>= 1.14.0)' \
               -d 'libstdc++6 (>= 5)' \
               -d 'libstdc++6 (>= 6)' \
               -d 'libx11-6' \
               -d 'libx11-6 (>= 2:1.4.99.1)' \
               -d 'libxcb1 (>= 1.9.2)' \
               -d 'libxcomposite1 (>= 1:0.4.4-1)' \
               -d 'libxdamage1 (>= 1:1.1)' \
               -d 'libxext6' \
               -d 'libxfixes3' \
               -d 'libxkbcommon0 (>= 0.5.0)' \
               -d 'libxkbfile1 (>= 1:1.1.0)' \
               -d 'libxrandr2' \
               -d 'xdg-utils (>= 1.0.2)' \
               --deb-recommends libvulkan1 \
               --maintainer 'VSCodium Team https://github.com/VSCodium/vscodium/graphs/contributors' \
               --deb-priority optional \
               --provides visual-studio-codium \
               --conflicts visual-studio-codium \
               --replaces visual-studio-codium \
               --url 'https://vscodium.com/' \
               --description 'VSCodium - Code editing. Redefined.' \
               --deb-no-default-config-files \
               --deb-compression xz \
               --after-install postinst \
               --before-remove prerm \
               --after-remove postrm \
               usr"
         }
      }
      stage('Archive') {
         steps {
            echo 'Archive Build'
            archiveArtifacts '*.deb'
         }
      }
   }
}
