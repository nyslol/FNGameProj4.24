cd ~/Downloads/plugin_src
rm -rf Bait && cp -r Faith Bait && cd Bait

# rename + credit the original
sed -i 's/Faith/Bait/g' source/main.cpp Makefile
sed -i '1i // Bait - based on Faith (FortOrbis / Tevtongermany)' source/main.cpp

# keep the shared headers inside the project instead of ../../core
sed -i 's|^\(COMMON_DIR[[:space:]]*:=\).*|\1 ../$(OUTPUT_PRX)/core|' Makefile
mkdir -p core/Logging/Public core/Kernal/Notification/Public

cat > core/core.h << 'EOF'
#pragma once
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdint.h>
#include <stdbool.h>
EOF

cat > core/Logging/Public/Log.h << 'EOF'
#pragma once
#include <stdio.h>
enum class LogVerbosity { Log, Warning, Error };
#define DECLARE_LOG_CATEGORY(Name) static const char *const Name = #Name
#define LOG(Category, Verbosity, ...) \
    do { printf("[%s] ", Category); printf(__VA_ARGS__); printf("\n"); } while (0)
EOF

echo '#pragma once' > core/Kernal/Notification/Public/notification.h

# set your server address
read -p "Server URL (e.g. http://192.168.1.14:3551): " URL
sed -i "s|^const char \*RedirectURL = .*|const char *RedirectURL = \"$URL\";|" source/main.cpp

make clean
make
