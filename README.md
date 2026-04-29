<p align="center"><img src="buildroot/share/pixmaps/logo/marlin-outrun-nf-500.png" height="250" alt="MarlinFirmware's logo" /></p>

<h1 align="center">Marlin 2.1.2 — Cliever CL2 Pro</h1>

Firmware customizado baseado no [Marlin 2.1.2](https://github.com/MarlinFirmware/Marlin) para a impressora 3D **Cliever CL2 Pro**, utilizando a placa-mãe **MKS Robin Nano V3.1** com drivers **TMC2209** em modo UART.

## Hardware

| Componente | Especificação |
|---|---|
| Placa-mãe | MKS Robin Nano V3.1 (STM32F407VET6) |
| Display | MKS TS35 V2.0 (TFT Color UI) |
| Drivers | TMC2209 (UART) |
| Extrusora | Extrusão direta, 1 hotend |
| Sensor de nivelamento | Probe manual (Z_MIN) |
| Armazenamento | USB Flash Drive (pendrive) |

## Área de Impressão

| Eixo | Dimensão |
|---|---|
| X | 300 mm |
| Y | 230 mm |
| Z | 215 mm |

## Principais Configurações

### Cinemática e Movimento

| Parâmetro | X | Y | Z | E |
|---|---|---|---|---|
| Steps/mm | 53.30 | 53.30 | 637.00 | 16.51 |
| Max Feedrate (mm/s) | 80 | 80 | 5 | 193.98 |
| Max Acceleration (mm/s²) | 800 | 800 | 25 | 1000 |

- **Print Acceleration:** 3000 mm/s²
- **Retract Acceleration:** 1000 mm/s²
- **Travel Acceleration:** 1500 mm/s²
- **Junction Deviation:** 0.15 mm

### Correntes dos Drivers (RMS)

| Driver | Corrente (mA) |
|---|---|
| X | 800 |
| Y | 800 |
| Z | 1100 |
| E | 700 |

### Recursos Habilitados

- **StealthChop** em todos os eixos (X, Y, Z, E)
- **Input Shaping:** X e Y a 40 Hz, damping 0.15
- **Linear Advance:** K = 0.30
- **Babystepping** habilitado
- **Auto Bed Leveling** (Bilinear, 3x3)
- **Z-Probe Offset:** -22.94 mm
- **USB Flash Drive** para leitura de G-code

## Compilação

### Requisitos

- [Visual Studio Code](https://code.visualstudio.com/) com a extensão [PlatformIO](https://platformio.org/)

### Build

O ambiente de compilação é `mks_robin_nano_v3_1_usb_flash_drive`:

```bash
pio run -e mks_robin_nano_v3_1_usb_flash_drive
```

O arquivo binário gerado será:
```
.pio/build/mks_robin_nano_v3_1_usb_flash_drive/Robin_nano_v3.bin
```

### Atualização do Firmware

1. Copie o arquivo `Robin_nano_v3.bin` para um pendrive formatado em FAT32.
2. Com a impressora desligada, insira o pendrive na porta USB da placa.
3. Ligue a impressora. O firmware será atualizado automaticamente.
4. Após a atualização, envie `M502` seguido de `M500` para carregar os novos valores padrão na EEPROM.

## Alteração da Altura Z

Para adaptar o firmware a variantes da impressora com diferentes alturas de Z (ex: 450 mm), basta alterar o parâmetro `Z_MAX_POS` no arquivo `Marlin/Configuration.h`:

```cpp
#define Z_MAX_POS 215   // Altura padrão (mm)
```

Nenhum outro parâmetro precisa ser modificado.

## Licença

Marlin é publicado sob a [licença GPL](/LICENSE). Consulte o arquivo LICENSE para mais detalhes.
