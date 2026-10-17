# Changelog

## 1.3.0

### Changed

- **Breaking:** `CBUSbase::begin()` no longer takes an `SPIClass` argument, and `CBUS.h` no longer includes `<SPI.h>`.

  Rationale: transports whose hardware has no SPI (ESP32 TWAI, STM32 bxCAN, RP2040 PIO) no longer have to accept and discard a dummy parameter, and the base class no longer depends on the SPI library or on the `ARDUINO_ARCH_RP2040` conditional that selected the SPI type.

  Migration for existing SPI-based subclasses: keep a `begin(bool poll, SPIClass &spi)` override (or a `setSPI()` setter) and add a one-argument `begin(bool poll)`. Callers that pass a custom `SPIClass` explicitly are unaffected.
