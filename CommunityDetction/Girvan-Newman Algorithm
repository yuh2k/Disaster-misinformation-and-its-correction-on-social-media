#coding=utf-8
import networkx as nx
import matplotlib.pyplot as plt
import util
import os
os.getcwd()

class GN(object):
	"""docstring for GN"""
	def __init__(self, G):
		self._G_cloned = util.clone_graph(G)
		self._G = G
		self._partition = [[n for n in G.nodes()]]
		self._max_Q = 0.0

	# G
	def execute(self):
		while len(self._G.edges()) > 0:
			#1.calculate the all the edge betweenness
			print("excute")
			edge = max(nx.edge_betweenness(self._G).items(), 
				key = lambda item:item[1])[0]
			# 2.remove the edge with largest betweenness
			self._G.remove_edge(edge[0], edge[1])

			components = [list(c) for c in list(nx.connected_components(self._G))]
			if len(components) != len(self._partition):
				# 3.calculate the Q value
				cur_Q = util.cal_Q(components, self._G_cloned)
				if cur_Q > self._max_Q:
					self._max_Q = cur_Q
					self._partition = components
		return self._partition

# visualize the partition
def showCommunity(G, partition, pos):
	print("start of showing community")

	cluster = {}
	labels = {}
	for index,item in enumerate(partition):
		for nodeID in item:
			labels[nodeID] = r'$' + str(nodeID) + '$' #visualize label
			cluster[nodeID] = index 

	# visualize the node
	colors = ['r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold',
				'r','g','b','y','c','turquoise','tomato','sandybrown','silver','sienna','seashell','seagreen','salmon',
				'violet','m','aliceblue','black','hotpink','lightcyan','navy','orangered','bisque','darkkhaki','gold']
	shapes = ['o']
	for index, item in enumerate(partition):
		nx.draw_networkx_nodes(G, pos, nodelist = item, 
			node_color = colors[index],
			node_shape = shapes[0],
			node_size = 1,
			alpha = 1)

	# visualize the edge
	edges = {len(partition):[]}
	cnt0 = 0
	for link in G.edges():
		cnt0 += 1
		print(cnt0)
		# links between clusters
		if cluster[link[0]] != cluster[link[1]]:
			edges[len(partition)].append(link)
		else:
			# links within the clusters
			if cluster[link[0]] not in edges:
				edges[cluster[link[0]]] = [link]
			else:
				edges[cluster[link[0]]].append(link)

	for index,edgelist in enumerate(edges.values()):
		# inside the cluster
		if index < len(partition):
			nx.draw_networkx_edges(G, pos, 
				edgelist = edgelist,
				width = 0.5, alpha = 0.8, edge_color = colors[index])
		else:
			# between the cluster
			nx.draw_networkx_edges(G, pos, 
				edgelist = edgelist,
				width = 0.5, alpha = 0.8, edge_color = colors[index])

	# visualize label
	nx.draw_networkx_labels(G, pos, labels, font_size = 0)

	plt.axis('off')
	plt.show()


if __name__ == '__main__':
	# load the network and visualize it
	G = util.load_graph("C:/sandy_NetworkX/CommunityDetection/network/retweet_code.txt")   # path
	pos = nx.spring_layout(G)
	nx.draw_networkx(G, with_labels = False, edge_color='b', node_color='r', width=0.1, node_size=0.05)
	plt.show()

	# GN algorithm
	algo = GN(G)
	partition = algo.execute()
	print(partition)
	with open('C:/sandy_NetworkX/CommunitiesPartition/partition.txt', 'w', encoding="utf-8") as f1:
		f1.write(str(partition))

	# visualize the outcome finally
	showCommunity(algo._G_cloned, partition, pos)

