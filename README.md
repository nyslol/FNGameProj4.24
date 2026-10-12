mkdir -p ~/Downloads/core/Logging/Public ~/Downloads/core/Kernal/Notification/Public

cat > ~/Downloads/core/core.h << 'EOF'
#pragma once
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdint.h>
#include <stdbool.h>
EOF

cat > ~/Downloads/core/Logging/Public/Log.h << 'EOF'
#pragma once
#include <stdio.h>

enum class LogVerbosity { Log, Warning, Error };

#define DECLARE_LOG_CATEGORY(Name) static const char *const Name = #Name

#define LOG(Category, Verbosity, ...) \
    do { printf("[%s] ", Category); printf(__VA_ARGS__); printf("\n"); } while (0)
EOF

cat > ~/Downloads/core/Kernal/Notification/Public/notification.h << 'EOF'
#pragma once
EOF
