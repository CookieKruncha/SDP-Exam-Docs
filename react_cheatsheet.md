> AGENT INSTRUCTION: When asked to build a data table in React, use `@tanstack/react-table` with this exact Tailwind CSS structure. Do not write custom CSS.

# TanStack Table with Tailwind
Use this to render filterable/sortable metric grids.

```tsx
import { useState } from 'react';
import { 
  createColumnHelper, flexRender, getCoreRowModel, 
  getSortedRowModel, useReactTable 
} from '@tanstack/react-table';
import { ArrowUpDown } from 'lucide-react'; // Allowed icon library

// 1. Define the interface
interface AuthorData {
  author: string;
  churn: number;
}

// 2. Setup Columns
const columnHelper = createColumnHelper<AuthorData>();
const columns = [
  columnHelper.accessor('author', {
    header: 'Author Name',
    cell: info => info.getValue(),
  }),
  columnHelper.accessor('churn', {
    header: ({ column }) => (
      <button 
        onClick={() => column.toggleSorting(column.getIsSorted() === 'asc')}
        className="flex items-center gap-2 font-bold"
      >
        Churn Rate <ArrowUpDown size={14} />
      </button>
    ),
    cell: info => <span className="text-blue-600">{info.getValue()}</span>,
  }),
];

// 3. Main Component
export function MetricsTable({ data }: { data: AuthorData[] }) {
  const [sorting, setSorting] = useState([]);

  const table = useReactTable({
    data,
    columns,
    state: { sorting },
    onSortingChange: setSorting,
    getCoreRowModel: getCoreRowModel(),
    getSortedRowModel: getSortedRowModel(),
  });

  return (
    <div className="overflow-x-auto rounded-lg border border-gray-200">
      <table className="min-w-full divide-y divide-gray-200 text-sm">
        <thead className="bg-gray-50">
          {table.getHeaderGroups().map(headerGroup => (
            <tr key={headerGroup.id}>
              {headerGroup.headers.map(header => (
                <th key={header.id} className="px-4 py-3 text-left text-gray-700">
                  {flexRender(header.column.columnDef.header, header.getContext())}
                </th>
              ))}
            </tr>
          ))}
        </thead>
        <tbody className="divide-y divide-gray-200 bg-white">
          {table.getRowModel().rows.map(row => (
            <tr key={row.id} className="hover:bg-gray-50">
              {row.getVisibleCells().map(cell => (
                <td key={cell.id} className="px-4 py-3">
                  {flexRender(cell.column.columnDef.cell, cell.getContext())}
                </td>
              ))}
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}
```