
# FASTDB: An Array Database System for Efficient Storing and Analyzing Massive Scientific Data
[源文件](http://pan.baidu.com/s/1b7BNMA)  

## Abstract
　　With the development of science and technology, the data size and
complexity of scientific data are increased rapidly, which made efficient data
storage and parallel analysis of scientific data become a big challenge. The
previous techniques that combine the traditional relational database with analysis
software tends cannot efficiently meet the performance requirement of large
scale scientific data based analysis. In this paper, we present FASTDB, a distributed
array database system that optimized for massive scientific data management
and provide a share-nothing, parallel array processing analysis. In order
to demonstrate the intrinsic performance characteristics of FASTDB, we applied
it into the interactive analysis of data from astronomical surveys, and designed a
series of experiments with scientific analysis tasks. According to the experimental
results, we found FASTDB can be significantly fast than traditional
database based SkyServer in many typical analytical scenarios.

## Introduction
　　With the development of science and technology, the volume of scientific data
approximately doubling every year. The relational database system have been widely
used and proved its values in various areas. However, as the scientific data has the
characteristic of high noise, massive computation and often prefer in array model in
nature, RDBMS tends cannot to be the satisfactory solution to achieve scalable analysis
and storage for data-intensive scientific areas [1, 2], e.g., astronomy survey like the
Sloan Digital Sky Survey (SDSS) [3, 23], which aiming at creating a digital map of a
big part of the universe by spectroscopic data. There are urgent needs to develop
efficient and scalable array model based scientific database systems for scientific areas.  
　　Given a concrete example, consider data from the five hundred meters Aperture
Spherical radio Telescope (FAST) [4], the world’s largest astronomical radio telescope.It can make the neutral hydrogen observation extends to the edge of the universe, make
dark matter and dark energy observations, enable the arrive time precision of pulsar
from the current 120 ns to 30 s and search for interstellar communication signal and
extraterrestrial civilizations, etc. The data such as the strength of the radio celestial
objects, spectrum and polarization data deriving from FAST has multidimensional
characteristics that cannot matched to traditional relational database. For example, the
process of cross-identification of multi-band radio data would merge multiple data sets,
then it will become more complicated when it comes to the matrix inverse operation.
　　To meet the requirements of large-scale scientific data storage and analysis, the
array model based database system have been proposed. It often provides with inherent
support for multi-dimensional arrays and opt for the array as the first-class citizen and it
is designed to be a share-nothing architecture [5–7].
　　In this paper, we present the analytical database system FASTDB [11], which
builds on array model based SciDB engine [8–10] to provide a share-nothing, parallel
processing and data management engine for needs of FAST [4]. In the internal of
database engine layer, we hacked its implementation to enhanced SciDB’s adaptive
storage capability. Furthermore, we optimized its parallel loading capability and
multiple join implementation, which can enable efficient complex astronomical data
analysis such as cross-identification.

