#Azure Dev / Test Labs
Provides some examples on how to deploy an Azure Dev / Test Lab

<ul>
<li><a href="#1-overview">1. Overview</a></li>
<li><a href="#2-provision-lab">2. Provision a Lab</a></li>
</ul>




<h2><a id="content-overview" class="anchor" href="#1-overview" aria-hidden="true">
<svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>1. Solution Overview</h2>

<blockquote>
<p>☛ As this solution is currently going through a formal review, we have kept this GitHub public repo  to be a temporary location. Post review, the solution would be made available in <a href="https://azure.microsoft.com/en-us/resources/templates/">Azure QuickStart</a> repo. For any questions, Please reach out to <a href="mailto:azurecompliance@avyanconsulting.com"></a><a href="mailto:azurecompliance@avyanconsulting.com">azurecompliance@avyanconsulting.com</a></p>
</blockquote>

<p>An integrated ARM Template (<a href="https://azure.microsoft.com/en-us/documentation/articles/resource-group-overview/">Azure Resource Manager</a>) that stitches all the above technology into a single deployment. The following is a feature table that is pulled together for your benefit.
Customers want</p>

<table><thead>
<tr>
<th align="left">Features</th>
<th align="left">Some Examples from the Solution</th>
</tr>
</thead><tbody>
<tr>
<td align="left">Resources on-demand</td>
<td align="left"><ul> <li> Azure Resource Manager based Templatized Solution  </li> </ul></td>
</tr>
<tr>
<td align="left">DevOps Manageability</td>
<td align="left"><ul> <li> Infrastructure as code </li>  <li> Bastion Host VM for Releases and other management tasks tat can't be done over DMZ network </li> <li> Operations Management Suite and associated solutions</li>  <li>Runbook Automation </li></ul></td>
</tr>
<tr>
<td align="left">Solution Scalability</td>
<td align="left"><ul> <li>Azure PaaS familiarity and Scale </li> <li>Solution can be easily extended for multi-region deployments </li> <li> Each layer can be scaled out appropriately </li> </ul></td>
</tr>
<tr>
<td align="left">Built-in Security</td>
<td align="left"><ul> <li> End-point protection using SSL  </li> <li> Network segmentation based on service roles</li> <li> DMZ and firewalls </li> <li>End-to-end encryption</li> <li>Active Directory Role Based Access </li> <li>Database Encryption features (TDE, Client-side encryption, data-masking, connection encryption and many more) </li> <li>Disabling deprecated TLS 1.0 and 1.1 across the board </li> <li> Diagnostics storage Encryption </li>  <li>and many more... </li></ul></td>
</tr>
<tr>
<td align="left">Conforming to compliance standards from get-go</td>
<td align="left"><ul> <li> PCI DSS 3.2 compliance from the outset.<p> ☛ Please have your QSA review the conformance to your specific Auditing and Implementation standards </p></li> </ul></td>
</tr>
<tr>
<td align="left">Integration</td>
<td align="left"><ul> <li>Azure Active Directory Integration </li> <li>Standardized Azure native Monitoring </li>  </ul></td>
</tr>
</tbody></table>




<h2><a id="#2-provision-lab" class="anchor" href="#2-provision-lab" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>2. Provision a Lab</h2>
