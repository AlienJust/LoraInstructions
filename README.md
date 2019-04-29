# LoraInstructions
Instructions for building loramac, written in Russian:
## Установка и настройка
1. Cmake, 
https://cmake.org/download/ (x64 installer)
во время установки установить флажок "Модифицировать переменную окружения (среды) PATH для всех юзеров"

2. ARM gcc compilers (SHA2 подписанные для Win7+, второй пункт в загруках)
**Качать надо не последнюю версию из-за бага: https://devzone.nordicsemi.com/f/nordic-q-a/43354/linker-error-address-out-of-range-for-intel-hex-files**. Качать 7 2018-q2-update: https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads
    
Отметить флажок на модификацию PATH (остальные тоже оставить отмеченными, разве что readme убрать)
Также модифицировать системную переменную среды PATH, добавив: C:\Program Files (x86)\GNU Tools ARM Embedded\8 2018-q4-major\bin
    
3. MSYS2
http://www.msys2.org (скачать инсталлятор x86_x64)
msys использует менеджер пакетов pacman (аналогично Arch Linux, Manjaro Linux)
в консольном окне MSYS2 выполнить:
  * pacman -Syu
  * закрыть окно (можно принудительно)
  * открыть окно используя ярлык меню Пуск -> MSYS2 MSYS и выполнить команды:
  * pacman -Su
  * pacman -S mingw-w64-x86_64-make
  * добавить в переменную среды системы PATH путь: C:\msys64\mingw64\bin

4.  Скачать неофициальную сборку openocd: 
    http://www.freddiechopin.info/en/download/category/4-openocd
    распаковать в C:\openocd\
    модифицировать переменную среды системы PATH, добавив C:\openocd\bin-x64\
    
5.  Скачать Visual Studio Code
установить расширения (ctrl + shift + x):
  * C/C++
  * CMake
  * CMake Tools
  * Native Debug

В настройка Visual Studio Code прописать (File->Preferences->Settings): 
UserSettings->Extensions->Cmake Configuration:
CMake path изменить на C:/PROGRA~1/CMake/bin/cmake.exe
чуть ниже выбрать пункт "Edit settings.json" и дописать строку: 
"cmake.preferredGenerators": ["MinGW Makefiles", "Ninja", "Unix Makefiles" ]
        
в итоге файл настроек VSCode settings.json будет выглядеть так: 
```json
{
    "cmake.cmakePath": "C:/PROGRA~1/CMake/bin/cmake.exe",
    "cmake.preferredGenerators": ["MinGW Makefiles", "Ninja", "Unix Makefiles" ]
}
```

6. Склонировать репозиторий https://github.com/Lora-net/LoRaMac-node.git
Переключиться на ветку feature/5.0.0
Открыть директорию репозитория в VSCode
Дождаться, пока расширение Cmake tools сгенерирует файлы
Добавить переменные файла .vscode/settings.json:
```json
"cmake.configureSettings": {
    ...
    "TOOLCHAIN_PREFIX":"C:/PROGRA~2/GNUTOO~1/72018-~1",
    "OPENOCD_BIN":"C:/openocd/bin-x64/openocd.exe",
    ...
}
```
