<!-- MADC_32.md --- 
;; 
;; Description: 
;; Author: Hongyi Wu(吴鸿毅)
;; Email: wuhongyi@qq.com 
;; Created: 六 2月 18 21:15:16 2017 (+0800)
;; Last-Updated: 日 7月  9 16:12:32 2017 (+0800)
;;           By: Hongyi Wu(吴鸿毅)
;;     Update #: 5
;; URL: http://wuhongyi.cn -->

# MADC-32  Fast 32 channel VME Peak sensing ADC

说明书 [MNV-3](http://wuhongyi.cn/DAQNote/pdf/ElectronicsModules/MESYTEC/MADC-32.pdf)

## Features

- High quality 11 to 13 bit (2, 4, 8 k) conversion with sliding scale ADC (DNL <1 % @ 4k)
- 800 ns, 1.6 us, 6.4 us conversion time for 32 channels wit 2 k, 4 k, 8 k resolution
- 8 k (32 bit-)words multi event buffer (1 word corresponds to 1 converted channel => 240...2730 events total)
- Zero suppression with individual thresholds
- Supports different types of time stamping
- Independent bank operation
- Two register adjustable gate generators are built in
- Input range, register selectable 4 V, 8 V, 10 V
- mesytec control bus to control external mesytec modules
- Address modes: A24 / A32
- Data transfer modes: D16 (registers), D32, BLT32, MBLT64, CBLT, CMBLT64
- Multicast for event reset and time stamping start
- Live insertion (can be inserted in a running crate)


## Technical Data

- Input / Output
	- Conversion input 1 kΩ, 4 V, 8 V or 10 V configurable via register
	- Rise time min.: 50 ns, max: DC-conversion possible
- ECL inputs
	- standard ECL input, can be individually terminated via register setting
- NIM inputs
	- standard NIM
- NIM output
	- -0.7 V terminated
mesytec control bus output, shares connector with busy output. +0.7 V terminated





Front Panel LEDs

- LED “Conv”  digitization in progress
- LED “Drdy”  Data are ready converted and can be read out
- LED “Nrdy”  Gate detected, but ADC busy. Event will be lost (should never happen in a well controlled DAQ). Or fast clear outside of acceptance window.
- LED “Dtack”  Access from VME bus accepted








<!-- MADC_32.md ends here -->
