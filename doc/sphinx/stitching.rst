Parallel Stitching and Ghost Cells
==================================

When visualizing partitioned unstructured grids, ParaView treats each
VTKHDF partition as a separate piece of geometry. To produce a seamless
visualization and ensure mathematical correctness across the global domain,
specifically named mesh-centered arrays may be written to the file.
When ParaView encounters these arrays, it interprets them as metadata
rather than ordinary point or cell data. These arrays are written using
the standard point and cell data procedures.

* ``"vtkGhostType"``: an ``int8`` cell-centered array identifying each cell
  as either a real cell owned by the local rank (value 0) or a ghost
  (duplicate) cell (value 1). This prevents duplicate cells from being
  rendered as overlapping geometry. While not required, ghost cells provide
  the context needed for filters to interpolate values across partition
  boundaries.

* ``"vtkGlobalPointIds"``: an ``int64`` point-centered array providing a
  unique global index for every node. This prevents visual "cracks" in
  filters such as Contour or Slice.

* ``"vtkGlobalCellIds"``: an ``int64`` cell-centered array providing a
  unique global index for every cell. This is required for accurate data
  integration (e.g., the Integrate Variables filter), ensuring that ghost
  or duplicate cells are not double-counted.
