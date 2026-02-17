Examples
========

A minimal usage pattern for writing an UnstructuredGrid file is:

.. code-block:: fortran

   use vtkhdf_ug_file_type
   type(vtkhdf_ug_file) :: file
   integer :: stat
   character(:), allocatable :: errmsg

   call file%create("mesh.vtkhdf", comm, stat, errmsg)
   call file%write_mesh(points, cnode, xcnode, types)
   call file%write_cell_data("pressure", pressure)
   call file%close()

This illustrates the required ordering of calls: create the file,
write the mesh, write any static or temporal datasets, and finally close.

More complete examples (serial and MPI-parallel, UnstructuredGrid and
MultiBlockDataSet) are provided in the ``examples`` directory of
the project repository.
