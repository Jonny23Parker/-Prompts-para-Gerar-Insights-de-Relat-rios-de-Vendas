Labs do Curso de Engenharia de Prompts DIO - criação de dataset de vendas

import React, { useState } from 'react';

// Constantes para prazos e ações
const PRAZOS = [
  'Curto Prazo (3 meses)',
  'Médio Prazo (6 meses)',
  'Longo Prazo (12 meses)',
];

const acoes = {
  'Curto Prazo (3 meses)': [
    {
      area: 'Preço e Promoção',
      acao: 'Implementar programa de descontos por volume',
      impacto: 'Alto',
      prioridade: 'Alta',
      mercados: 'Todos',
    },
    {
      area: 'Capacitação',
      acao: 'Treinar equipe de vendas sobre diferenciais do produto',
      impacto: 'Médio',
      prioridade: 'Alta',
      mercados: 'Todos',
    },
    {
      area: 'Marketing',
      acao: 'Lançar campanhas promocionais nos mercados principais',
      impacto: 'Alto',
      prioridade: 'Alta',
      mercados: 'Japão, França',
    },
    {
      area: 'Vendas',
      acao: 'Criar programa de incentivo para vendedores',
      impacto: 'Médio',
      prioridade: 'Média',
      mercados: 'Todos',
    },
  ],
  'Médio Prazo (6 meses)': [
    {
      area: 'Marketing',
      acao: 'Desenvolver materiais específicos por região',
      impacto: 'Alto',
      prioridade: 'Média',
      mercados: 'Todos',
    },
    {
      area: 'Vendas',
      acao: 'Implementar programa de fidelidade',
      impacto: 'Alto',
      prioridade: 'Média',
      mercados: 'Europa, Japão',
    },
    {
      area: 'Parcerias',
      acao: 'Expandir rede de revendedores',
      impacto: 'Alto',
      prioridade: 'Média',
      mercados: 'Alemanha, Austrália',
    },
    {
      area: 'Produto',
      acao: 'Desenvolver bundles com produtos complementares',
      impacto: 'Médio',
      prioridade: 'Média',
      mercados: 'Todos',
    },
  ],
  'Longo Prazo (12 meses)': [
    {
      area: 'Expansão',
      acao: 'Avaliar entrada em novos mercados',
      impacto: 'Alto',
      prioridade: 'Baixa',
      mercados: 'Novos',
    },
    {
      area: 'Produto',
      acao: 'Desenvolver versões específicas por mercado',
      impacto: 'Alto',
      prioridade: 'Média',
      mercados: 'Todos',
    },
    {
      area: 'CRM',
      acao: 'Implementar programa de relacionamento',
      impacto: 'Alto',
      prioridade: 'Média',
      mercados: 'Todos',
    },
    {
      area: 'Operacional',
      acao: 'Otimizar gestão de estoque por região',
      impacto: 'Médio',
      prioridade: 'Alta',
      mercados: 'Todos',
    },
  ],
};

// Funções auxiliares para obter as classes de badge

const getImpactBadgeClass = (impacto) => {
  if (impacto === 'Alto') return 'bg-green-100 text-green-800';
  if (impacto === 'Médio') return 'bg-yellow-100 text-yellow-800';
  return 'bg-red-100 text-red-800';
};

const getPrioridadeBadgeClass = (prioridade) => {
  if (prioridade === 'Alta') return 'bg-red-100 text-red-800';
  if (prioridade === 'Média') return 'bg-yellow-100 text-yellow-800';
  return 'bg-green-100 text-green-800';
};

// Componente que renderiza a tabela de ações para um prazo específico
const ActionTable = ({ prazo, actions }) => (
  <div className="mb-8">
    <h3 className="text-lg font-semibold mb-3 bg-gray-100 p-2">{prazo}</h3>
    <div className="overflow-x-auto">
      <table className="min-w-full bg-white border border-gray-300">
        <thead>
          <tr className="bg-gray-50">
            <th className="px-6 py-3 border-b text-left">Área</th>
            <th className="px-6 py-3 border-b text-left">Ação</th>
            <th className="px-6 py-3 border-b text-center">Impacto</th>
            <th className="px-6 py-3 border-b text-center">Prioridade</th>
            <th className="px-6 py-3 border-b text-left">Mercados</th>
          </tr>
        </thead>
        <tbody>
          {actions.map((acao, idx) => (
            <tr key={idx} className={idx % 2 === 0 ? 'bg-white' : 'bg-gray-50'}>
              <td className="px-6 py-4 border-b">{acao.area}</td>
              <td className="px-6 py-4 border-b">{acao.acao}</td>
              <td className="px-6 py-4 border-b text-center">
                <span className={`px-2 py-1 rounded text-sm ${getImpactBadgeClass(acao.impacto)}`}>
                  {acao.impacto}
                </span>
              </td>
              <td className="px-6 py-4 border-b text-center">
                <span className={`px-2 py-1 rounded text-sm ${getPrioridadeBadgeClass(acao.prioridade)}`}>
                  {acao.prioridade}
                </span>
              </td>
              <td className="px-6 py-4 border-b">{acao.mercados}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  </div>
);

// Componente principal do Plano Estratégico
const PlanoEstrategico = () => {
  const [filtroAtivo, setFiltroAtivo] = useState('todos');

  return (
    <div className="p-4">
      <h2 className="text-xl font-bold mb-4">Plano de Ação Estratégico - MEGANIUM RG353M</h2>
      
      <div className="mb-4">
        <label htmlFor="prazoFilter" className="mr-2 font-medium">Filtrar por prazo:</label>
        <select 
          id="prazoFilter"
          className="border p-2 rounded"
          value={filtroAtivo}
          onChange={(e) => setFiltroAtivo(e.target.value)}
        >
          <option value="todos">Todos os prazos</option>
          {PRAZOS.map(prazo => (
            <option key={prazo} value={prazo}>{prazo}</option>
          ))}
        </select>
      </div>

      {PRAZOS.map((prazo) =>
        (filtroAtivo === 'todos' || filtroAtivo === prazo) && (
          <ActionTable key={prazo} prazo={prazo} actions={acoes[prazo]} />
        )
      )}
    </div>
  );
};

export default PlanoEstrategico;
