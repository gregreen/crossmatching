crossmatching
=============

Simple divide-and-conquer algorithm for cross-matching astronomical catalogs. The goal is to match each entry in an overlay catalog to its nearest neighbor in a base catalog, subject to some maximum matching distance.

First, both the base catalog and overlay catalog are partitioned into HEALPix pixels. The base catalog may be partitioned at higher resolution than the overlay catalog. For each HEALPix pixel in the overlay catalog, a slightly larger (one HEALPix pixel in the base catalog pixelization) patch is selected from the base catalog. The closest matches (between the base and overlay patches) are then identified by brute force. This is repeated for each HEALPix pixel in the overlay catalog, and the indices of all the identified matches in the base and overlay catalogs are returned.

A minimal example might look as follows. It is assumed that `lon_base`, `lat_base`, `lon_over` and `lat_over` are arrays of `astropy` `Quantity` objects, representing the coordinates in the base and overlay catalogs, and that `dmax` is the maximum matching distance (likewise stored as a `Quantity` object):

```python
from crossmatch import HEALPixCatalog, match_catalogs

nside_base = 16
base_cat = HEALPixCatalog(lon_base, lat_base, nside_base)

nside_over = 8
over_cat = HEALPixCatalog(lon_over, lat_over, nside_over)

idx_match_base, idx_match_over, dist = match_catalogs(base_cat, over_cat, dmax)
```

There is an example implementation in the `main()` function of `crossmatch.py`.


Dependencies
------------

* `numpy`
* `astropy`
* `astropy_healpix`

