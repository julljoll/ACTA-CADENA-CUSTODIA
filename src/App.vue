<template>
  <div class="min-h-screen bg-[#008080] p-4 sm:p-8 flex items-center justify-center print:p-8">
    <div class="win95-raised w-full max-w-[8.5in] p-[2px] shadow-[1px_1px_#000] print:shadow-none print:w-full">
      <!-- Title Bar -->
      <div class="win95-titlebar no-print">
        <div class="flex items-center gap-2">
          <FileText :size="14" />
          <span>Planilla de Registro de Cadena de Custodia</span>
        </div>
        <div class="flex gap-1">
          <button class="win95-button !min-w-0 w-4 h-4 p-0 flex items-center justify-center text-[10px]">_</button>
          <button class="win95-button !min-w-0 w-4 h-4 p-0 flex items-center justify-center text-[10px]">□</button>
          <button class="win95-button !min-w-0 w-4 h-4 p-0 flex items-center justify-center text-[10px]">X</button>
        </div>
      </div>      <!-- Main Content -->
      <div class="bg-[#c0c0c0] p-4 text-black print:p-4">
        
        <!-- PAGE 1: Header + I + II -->
        <div class="print:break-after-page print:min-h-[9.5in]">
          <!-- Screen Header -->
          <div class="flex flex-col md:flex-row items-center justify-between mb-8 gap-4 border-b-2 border-white pb-4 print:hidden">
            <div class="flex flex-col items-start gap-1">
              <span class="text-4xl font-black tracking-tighter text-[#161b2a]">SHA256.US</span>
              <span class="text-[8px] font-bold text-[#000080] uppercase tracking-tight max-w-[200px] leading-tight mt-1">LABORATORIO DE INFORMÁTICA FORENSE Y CIBERSEGURIDAD SHA256.US</span>
              <span class="text-[8px] font-medium text-gray-700 leading-tight max-w-[280px]">Avenida 6, con calle 7, Edificio Mercantil La Ceiba, primer piso, oficina Nº 8, Quibor, Municipio Jiménez del Estado Lara.</span>
            </div>
            <div class="text-right">
              <h1 class="text-xl font-bold bg-[#000080] text-white px-4 py-1 inline-block uppercase tracking-tighter">
                CADENA DE CUSTODIA (PRCC)
              </h1>
              <p class="text-[10px] mt-1 font-bold uppercase tracking-widest">Planilla de Registro de Evidencias</p>
            </div>
          </div>

          <!-- PRINT HEADER (matches PDF) -->
          <div class="hidden print:flex w-full justify-between items-start mb-8 pb-4 border-b border-gray-200">
            <div class="flex flex-col">
              <div class="flex items-stretch gap-3 mb-6">
                <div class="w-1.5 bg-black"></div>
                <div class="flex flex-col justify-center gap-1">
                  <span class="text-[10px] font-bold text-gray-500 tracking-wider">REGISTRO DE EXPEDIENTE NO.</span>
                  <span class="text-2xl font-black tracking-widest uppercase">EXP - {{ formData.expediente || '_______________' }}</span>
                </div>
              </div>
              <h1 class="text-2xl font-bold tracking-tight mb-2">PLANILLA DE REGISTRO DE CADENA DE CUSTODIA (PRCC)</h1>
              <h2 class="text-[11px] font-bold tracking-widest uppercase mb-1">LABORATORIO DE INFORMÁTICA FORENSE Y CIBERSEGURIDAD SHA256.US</h2>
              <p class="text-[10px] text-gray-700 uppercase max-w-[500px] leading-relaxed">
                Avenida 6, con calle 7, Edificio Mercantil La Ceiba, primer piso, oficina Nº 8, Quibor, Municipio Jiménez del Estado Lara.
              </p>
            </div>
            <div class="flex flex-col items-end">
              <span class="text-4xl font-black italic tracking-tighter">SHA256 <span class="font-light">.US</span></span>
              <span class="text-[12px] text-gray-500 tracking-wide mt-1">laboratorio forense</span>
            </div>
          </div>

          <!-- Section I -->
          <div class="section-group">
            <span class="section-label">I. DATOS GENERALES</span>
            <div class="hidden print:block bg-[#000080] text-white py-1.5 px-3 font-bold text-[12px] mb-4 text-center tracking-widest">
              I. DATOS GENERALES
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-x-6 gap-y-4">
              <div v-for="(field, label) in {
                'a. N° de Expediente': { key: 'expediente', placeholder: 'P.ej: MP-215-2023', type: 'text' },
                'b. N° PRCC': { key: 'prcc', placeholder: 'P.ej: 0001', type: 'text' },
                'c. Despacho que instruye': { key: 'despachoInstruye', placeholder: 'P.ej: Fiscalía 23°', type: 'text' },
                'd. Organismo que investiga e instructivo': { key: 'organismoInvestiga', placeholder: 'P.ej: CICPC', type: 'text' },
                'e. Despacho que inicia la custodia': { key: 'despachoCustodia', placeholder: 'P.ej: Div. Delitos Informáticos', type: 'text' },
                'f. Organismo que custodia': { key: 'organismoCustodia', placeholder: 'P.ej: SEBIN', type: 'text' },
                'g. Dirección de Obtención': { key: 'direccionObtencion', placeholder: 'Dirección exacta del sitio', type: 'text' },
                'h. Fecha y Hora': { key: 'fechaHora', placeholder: '', type: 'datetime-local' }
              }" :key="label" class="space-y-1">
                <label class="label-text print:text-[9px] print:font-bold print:uppercase print:tracking-wider print:text-gray-600">{{label}}</label>
                <div class="win95-sunken px-2 py-1 print:px-0">
                  <input 
                    :type="field.type" 
                    v-model="formData[field.key]" 
                    :placeholder="field.placeholder" 
                    class="w-full outline-none bg-transparent placeholder:text-gray-400 placeholder:italic text-[11px] print:font-bold print:text-[13px]" 
                  />
                </div>
              </div>
            </div>
          </div>

          <!-- Section II -->
          <div class="section-group">
            <span class="section-label">II. FORMAS DE OBTENCIÓN DE LA EVIDENCIA</span>
            <div class="hidden print:block bg-[#000080] text-white py-1.5 px-3 font-bold text-[12px] mb-4 text-center tracking-widest">
              II. FORMAS DE OBTENCIÓN DE LA EVIDENCIA
            </div>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
              <div v-for="(label, num) in {'1': 'Técnica', '2': 'Aseguramiento', '3': 'Consignación', '4': 'Derivación'}" :key="num" 
                  @click="toggleObtencion(num)"
                  class="flex items-center gap-2 cursor-pointer select-none">
                <span class="font-bold print:text-[11px]">{{num}}. {{label}}</span>
                <div :class="['w-4 h-4 win95-sunken print-checkbox flex items-center justify-center', obtencion[num] ? 'bg-white' : 'bg-gray-100']">
                  <div v-if="obtencion[num]" class="w-2 h-2 bg-black flex-shrink-0"></div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- PAGE 2: Section III -->
        <div class="print:break-after-page print:min-h-[10in]">
          <!-- Minimal Header for Page 2 -->
          <div class="hidden print:flex w-full justify-between items-end mb-6 pb-2 border-b border-gray-200">
            <span class="text-[10px] font-bold text-gray-500 tracking-wider">REGISTRO DE EXPEDIENTE NO. EXP - {{ formData.expediente || '_______________' }}</span>
            <span class="text-2xl font-black italic tracking-tighter">SHA256 <span class="font-light">.US</span></span>
          </div>

          <div class="section-group">
            <span class="section-label">III. FUNCIONARIO QUE OBTIENE LA EVIDENCIA</span>
            <div class="hidden print:block bg-[#000080] text-white py-1.5 px-3 font-bold text-[12px] mb-4 text-center tracking-widest">
              III. FUNCIONARIO QUE OBTIENE LA EVIDENCIA
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div v-for="title in ['PROTECCIÓN', 'OBSERVACIÓN PRELIMINAR', 'FIJACIÓN', 'COLECCIÓN']" :key="title" class="win95-raised p-4">
                <h4 class="bg-[#000080] text-white px-2 mb-4 font-bold">{{title}}</h4>
                <div class="space-y-3 mb-4">
                  <div class="space-y-1">
                    <span class="text-[10px] font-bold">a. Nombres y Apellidos:</span>
                    <div class="win95-sunken px-2 py-0.5">
                      <input type="text" placeholder="P.ej: Juan Pérez" class="w-full outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
                    </div>
                  </div>
                  <div class="space-y-1">
                    <span class="text-[10px] font-bold">b. C.I.:</span>
                    <div class="win95-sunken px-2 py-0.5">
                      <input type="text" placeholder="P.ej: V-12.345.678" class="w-full outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
                    </div>
                  </div>
                </div>
                <div class="grid grid-cols-3 gap-2">
                  <div class="space-y-1">
                    <div class="win95-sunken print-box h-20 flex items-center justify-center"></div>
                    <span class="block text-[8px] italic">c. Firma</span>
                  </div>
                  <div class="space-y-1">
                    <div class="win95-sunken print-box h-20 flex items-center justify-center"><Fingerprint :size="16" class="opacity-10" /></div>
                    <span class="block text-[8px] italic">Pulgar Izquierdo</span>
                  </div>
                  <div class="space-y-1">
                    <div class="win95-sunken print-box h-20 flex items-center justify-center"><Fingerprint :size="16" class="opacity-10" /></div>
                    <span class="block text-[8px] italic">Pulgar Derecho</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- PAGE 3: Section VI + V -->
        <div class="print:min-h-[10in]">
          <!-- Minimal Header for Page 3 -->
          <div class="hidden print:flex w-full justify-between items-end mb-6 pb-2 border-b border-gray-200">
            <span class="text-[10px] font-bold text-gray-500 tracking-wider">REGISTRO DE EXPEDIENTE NO. EXP - {{ formData.expediente || '_______________' }}</span>
            <span class="text-2xl font-black italic tracking-tighter">SHA256 <span class="font-light">.US</span></span>
          </div>

          <!-- Section VI -->
          <div class="section-group">
            <span class="section-label">VI. DESCRIPCIÓN DE LA EVIDENCIA</span>
            <div class="hidden print:block bg-[#000080] text-white py-1.5 px-3 font-bold text-[12px] mb-4 text-center tracking-widest">
              VI. DESCRIPCIÓN DE LA EVIDENCIA
            </div>
            <div class="win95-sunken relative pb-6">
              <div v-for="n in 7" :key="n" :class="['border-b border-gray-300 last:border-0 flex items-center px-4 py-1', n % 2 === 0 ? 'bg-gray-100' : 'bg-white']">
                <span class="w-8 font-bold text-gray-500">{{n}}</span>
                <input type="text" placeholder="Marca, Modelo, Serial, Color, Estado..." class="flex-1 outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
              </div>
              <div class="absolute bottom-1 right-2 flex items-center gap-2">
                <span class="text-[10px] font-bold uppercase">(Anexo A)</span>
                <div class="w-4 h-4 win95-sunken print-checkbox bg-white border cursor-pointer flex items-center justify-center">
                  <!-- Checkbox area, user can click or mark -->
                </div>
              </div>
            </div>
          </div>

          <!-- Section V -->
          <div class="section-group">
            <span class="section-label">V. TRANSFERENCIA DE EVIDENCIA</span>
            <div class="hidden print:block bg-[#000080] text-white py-1.5 px-3 font-bold text-[12px] mb-4 text-center tracking-widest">
              V. TRANSFERENCIA DE EVIDENCIA
            </div>
            <div class="mb-4 space-y-2">
              <label class="label-text">a. MOTIVO:</label>
              <div class="grid grid-cols-2 md:grid-cols-5 gap-2">
                <div v-for="(motivo, i) in ['Traslado', 'Peritaje', 'Resguardo', 'Disposición Judicial', 'Disposición Final']" :key="motivo" class="flex items-center gap-2">
                  <div class="w-4 h-4 win95-sunken print-checkbox bg-white"></div>
                  <span class="text-[11px] font-bold">{{i+1}}. {{motivo}}</span>
                </div>
              </div>
              <div class="flex items-center gap-2 mt-2">
                <label class="text-[10px] font-bold">Fecha y Hora:</label>
                <div class="win95-sunken px-2 py-0.5 w-48">
                  <input type="datetime-local" class="w-full outline-none bg-transparent text-[11px]" />
                </div>
              </div>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div v-for="(title, idx) in ['B. ENTREGA', 'C. RECIBE']" :key="title" class="win95-raised p-4">
                <h4 class="bg-[#000080] text-white px-2 mb-4 font-bold">{{title}}</h4>
                <div class="space-y-2 mb-4">
                  <div class="space-y-1">
                    <span class="text-[10px] font-bold">a. Nombres y Apellidos:</span>
                    <div class="win95-sunken px-2">
                      <input type="text" placeholder="Nombres y apellidos completos..." class="w-full outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
                    </div>
                  </div>
                  <div class="space-y-1">
                    <span class="text-[10px] font-bold">b. Organismo:</span>
                    <div class="win95-sunken px-2">
                      <input type="text" placeholder="Ej: CICPC..." class="w-full outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
                    </div>
                  </div>
                  <div class="space-y-1">
                    <span class="text-[10px] font-bold">c. Despacho:</span>
                    <div class="win95-sunken px-2">
                      <input type="text" placeholder="Despacho o división..." class="w-full outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
                    </div>
                  </div>
                  <div class="space-y-1">
                    <span class="text-[10px] font-bold">d. C.I./Cred:</span>
                    <div class="win95-sunken px-2">
                      <input type="text" placeholder="Cédula o credencial..." class="w-full outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
                    </div>
                  </div>
                  <div class="space-y-1">
                    <span class="text-[10px] font-bold">e. Fecha:</span>
                    <div class="win95-sunken px-2">
                      <input type="date" class="w-full outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
                    </div>
                  </div>
                </div>
                <div class="grid grid-cols-3 gap-2">
                  <div class="space-y-1">
                    <div class="win95-sunken print-box h-16 flex items-center justify-center"></div>
                    <span class="block text-[8px] italic">f. Firma</span>
                  </div>
                  <div class="space-y-1">
                    <div class="win95-sunken print-box h-16 flex items-center justify-center"><Fingerprint :size="16" class="opacity-10" /></div>
                    <span class="block text-[8px] italic">Pulgar Izquierdo</span>
                  </div>
                  <div class="space-y-1">
                    <div class="win95-sunken print-box h-16 flex items-center justify-center"><Fingerprint :size="16" class="opacity-10" /></div>
                    <span class="block text-[8px] italic">Pulgar Derecho</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Section D -->
          <div class="section-group">
            <span class="section-label">D. OBSERVACIÓN</span>
            <div class="hidden print:block bg-[#000080] text-white py-1.5 px-3 font-bold text-[12px] mb-4 text-center tracking-widest">
              D. OBSERVACIÓN
            </div>
            <div class="win95-sunken mb-4">
              <div v-for="n in 7" :key="n" :class="['border-b border-gray-300 last:border-0 flex items-center px-4 py-1', n % 2 === 0 ? 'bg-gray-100' : 'bg-white']">
                <span class="w-8 font-bold text-gray-500">{{n}}</span>
                <input type="text" class="flex-1 outline-none bg-transparent text-[11px]" />
              </div>
            </div>
            <div class="flex items-start gap-2 select-none">
              <div class="w-4 h-4 win95-sunken print-checkbox bg-white border cursor-pointer mt-0.5 flex-shrink-0 flex items-center justify-center"></div>
              <span class="text-[9px] leading-tight font-bold text-gray-700">
                Nota: la planilla de Registro de Cadena de Custodia debe permanecer siempre con la evidencia, y sólo en original, desde el instante de su llenado en el lugar de obtención hasta la disposición final de la evidencia.
              </span>
            </div>
          </div>
        </div>

        <!-- Footer Actions -->
        <div class="mt-8 flex justify-end no-print">
          <button @click="printDoc" class="win95-button flex items-center gap-2">
            <Printer :size="16" />
            IMPRIMIR REGISTRO
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { 
  FileText, 
  Printer, 
  Fingerprint
} from 'lucide-vue-next'

const formData = ref<Record<string, string>>({
  expediente: '',
  prcc: '',
  despachoInstruye: '',
  organismoInvestiga: '',
  despachoCustodia: '',
  organismoCustodia: '',
  direccionObtencion: '',
  fechaHora: new Date().toISOString().slice(0, 16),
})

const obtencion = ref<Record<string, boolean>>({
  '1': false,
  '2': false,
  '3': false,
  '4': false,
})

const toggleObtencion = (id: string) => {
  obtencion.value[id] = !obtencion.value[id]
}

const printDoc = () => {
  window.print()
}
</script>
