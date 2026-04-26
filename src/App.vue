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
          <!-- Header -->
          <div class="flex flex-col md:flex-row items-center justify-between mb-8 gap-4 border-b-2 border-white pb-4 print:border-black">
            <div class="flex flex-col items-start">
              <span class="text-4xl font-black tracking-tighter text-[#161b2a]">SHA256.US</span>
              <span class="text-[8px] font-bold text-[#000080] uppercase tracking-tight mt-0.5 max-w-[200px] leading-tight">LABORATORIO DE INFORMÁTICA FORENSE Y CIBERSEGURIDAD SHA256.US</span>
            </div>
            <div class="text-right">
              <h1 class="text-xl font-bold bg-[#000080] text-white px-4 py-1 inline-block uppercase tracking-tighter print:text-black print:bg-transparent">
                CADENA DE CUSTODIA (PRCC)
              </h1>
              <p class="text-[10px] mt-1 font-bold uppercase tracking-widest">Planilla de Registro de Evidencias</p>
            </div>
          </div>

          <!-- Section I -->
          <div class="section-group">
            <span class="section-label">I. DATOS GENERALES</span>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-x-6 gap-y-4">
              <div v-for="(field, label) in {
                'a. N° de Expediente': { key: 'expediente', placeholder: 'P.ej: MP-215-2023', type: 'text' },
                'b. N° PRCC': { key: 'prcc', placeholder: 'P.ej: 0001', type: 'text' },
                'c. Despacho que instruye': { key: 'despachoInstruye', placeholder: 'P.ej: Fiscalía 23°', type: 'text' },
                'd. Organismo que investiga': { key: 'organismoInvestiga', placeholder: 'P.ej: CICPC', type: 'text' },
                'e. Despacho que inicia custodia': { key: 'despachoCustodia', placeholder: 'P.ej: Div. Delitos Informáticos', type: 'text' },
                'f. Organismo que custodia': { key: 'organismoCustodia', placeholder: 'P.ej: SEBIN', type: 'text' },
                'g. Dirección de Obtención': { key: 'direccionObtencion', placeholder: 'Dirección exacta del sitio', type: 'text' },
                'h. Fecha y Hora': { key: 'fechaHora', placeholder: '', type: 'datetime-local' }
              }" :key="label" class="space-y-1">
                <label class="label-text">{{label}}:</label>
                <div class="win95-sunken px-2 py-1">
                  <input 
                    :type="field.type" 
                    v-model="formData[field.key]" 
                    :placeholder="field.placeholder" 
                    class="w-full outline-none bg-transparent placeholder:text-gray-400 placeholder:italic text-[11px]" 
                  />
                </div>
              </div>
            </div>
          </div>

          <!-- Section II -->
          <div class="section-group">
            <span class="section-label">II. FORMA DE OBTENCIÓN</span>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
              <div v-for="(label, num) in {'1': 'Técnica', '2': 'Aseguramiento', '3': 'Consignación', '4': 'Derivación'}" :key="num" 
                  @click="toggleObtencion(num)"
                  class="flex items-center gap-2 cursor-pointer select-none">
                <div :class="['w-4 h-4 win95-sunken flex items-center justify-center', obtencion[num] ? 'bg-white' : 'bg-gray-100']">
                  <div v-if="obtencion[num]" class="w-2 h-2 bg-black"></div>
                </div>
                <span class="font-bold">{{num}}. {{label}}</span>
              </div>
            </div>
          </div>
        </div>

        <!-- PAGE 2: Section III -->
        <div class="print:break-after-page print:min-h-[10in]">
          <!-- Minimal Header for Page 2 -->
          <div class="hidden print:flex items-center justify-between mb-6 border-b border-gray-400 pb-2">
            <span class="text-xl font-black text-[#161b2a]">SHA256.US</span>
            <span class="text-[10px] font-bold">REGISTRO DE CADENA DE CUSTODIA - SECCIÓN III</span>
          </div>

          <div class="section-group">
            <span class="section-label">III. FUNCIONARIO QUE OBTIENE</span>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div v-for="title in ['PROTECCIÓN', 'OBSERVACIÓN PRELIMINAR', 'FIJACIÓN', 'COLECCIÓN']" :key="title" class="win95-raised p-4">
                <h4 class="bg-[#000080] text-white px-2 mb-4 font-bold">{{title}}</h4>
                <div class="space-y-3 mb-4">
                  <div class="space-y-1">
                    <span class="text-[10px] font-bold">Nombres y Apellidos:</span>
                    <div class="win95-sunken px-2 py-0.5">
                      <input type="text" placeholder="P.ej: Juan Pérez" class="w-full outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
                    </div>
                  </div>
                  <div class="space-y-1">
                    <span class="text-[10px] font-bold">C.I.:</span>
                    <div class="win95-sunken px-2 py-0.5">
                      <input type="text" placeholder="P.ej: V-12.345.678" class="w-full outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
                    </div>
                  </div>
                </div>
                <div class="grid grid-cols-3 gap-2">
                  <div class="win95-sunken h-20 flex items-center justify-center text-[10px] text-gray-400 italic">Firma</div>
                  <div class="win95-sunken h-20 flex items-center justify-center"><Fingerprint :size="16" class="opacity-10" /></div>
                  <div class="win95-sunken h-20 flex items-center justify-center"><Fingerprint :size="16" class="opacity-10" /></div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- PAGE 3: Section VI + V -->
        <div class="print:min-h-[10in]">
          <!-- Minimal Header for Page 3 -->
          <div class="hidden print:flex items-center justify-between mb-6 border-b border-gray-400 pb-2">
            <span class="text-xl font-black text-[#161b2a]">SHA256.US</span>
            <span class="text-[10px] font-bold">REGISTRO DE CADENA DE CUSTODIA - SECCIONES VI, V</span>
          </div>

          <!-- Section VI -->
          <div class="section-group">
            <span class="section-label">VI. DESCRIPCIÓN DE LA EVIDENCIA</span>
            <div class="win95-sunken">
              <div v-for="n in 12" :key="n" class="border-b border-gray-300 last:border-0 flex items-center px-4 py-1">
                <span class="w-8 font-bold text-gray-500">{{n}}</span>
                <input type="text" placeholder="Marca, Modelo, Serial, Color, Estado..." class="flex-1 outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
              </div>
            </div>
          </div>

          <!-- Section V -->
          <div class="section-group">
            <span class="section-label">V. TRANSFERENCIA DE EVIDENCIA</span>
            <div class="mb-4">
              <label class="label-text">MOTIVO:</label>
              <div class="grid grid-cols-2 md:grid-cols-5 gap-2">
                <div v-for="motivo in ['Traslado', 'Peritaje', 'Resguardo', 'Judicial', 'Final']" :key="motivo" disabled class="flex items-center gap-2 opacity-50">
                  <div class="w-4 h-4 win95-sunken"></div>
                  <span class="text-[11px]">{{motivo}}</span>
                </div>
              </div>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div v-for="title in ['ENTREGA', 'RECIBE']" :key="title" class="win95-raised p-4">
                <h4 class="bg-[#000080] text-white px-2 mb-4 font-bold">{{title}}</h4>
                <div class="space-y-2 mb-4">
                  <div class="space-y-1">
                    <span class="text-[10px] font-bold">Nombres:</span>
                    <div class="win95-sunken px-2">
                      <input type="text" placeholder="P.ej: Pedro Rojas" class="w-full outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
                    </div>
                  </div>
                  <div class="space-y-1">
                    <span class="text-[10px] font-bold">Organismo:</span>
                    <div class="win95-sunken px-2">
                      <input type="text" placeholder="P.ej: Cuerpo de Investigaciones" class="w-full outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
                    </div>
                  </div>
                  <div class="space-y-1">
                    <span class="text-[10px] font-bold">Fecha:</span>
                    <div class="win95-sunken px-2">
                      <input type="text" placeholder="DD/MM/AAAA" class="w-full outline-none bg-transparent placeholder:text-gray-400 text-[11px]" />
                    </div>
                  </div>
                </div>
                <div class="grid grid-cols-3 gap-2">
                  <div class="win95-sunken h-16 flex items-center justify-center text-[8px] italic">Firma</div>
                  <div class="win95-sunken h-16"></div>
                  <div class="win95-sunken h-16"></div>
                </div>
              </div>
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
